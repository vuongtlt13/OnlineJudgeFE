<template>
  <Panel shadow :padding="10">
    <div slot="title">
      {{ title }}
    </div>
    <template>
      <ul class="announcements-container" key="list">
        <li v-for="problem in problems" :key="problem._id">
          <div class="flex-container">
            <div class="title">
              <a class="entry" @click="goToProblem(problem._id)">{{ problem.title }}</a>
            </div>
          </div>
        </li>
      </ul>
    </template>
  </Panel>
</template>

<script>
import api from '@oj/api'

export default {
  name: 'NewProblem',
  components: {},
  props: {
    limit: {
      type: Number,
      default: 10
    }
  },
  data () {
    return {
      problems: []
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {
      this.getNewestProblems(this.limit)
    },
    getNewestProblems (limit) {
      api.fetchNewestProblems(limit).then(res => {
        this.problems = res.data.data.problems
      }, () => {
      })
    },
    goToProblem (problemId) {
      this.$router.push({ name: 'problem-details', params: {
          problemID: problemId
        }})
    }
  },
  computed: {
    title () {
      return this.$i18n.t('m.Top_Newest_Problems')
    }
  }
}
</script>

<style scoped lang="less">
.announcements-container {
  margin-top: -10px;
  margin-bottom: 10px;
  padding-left: 16px;

  li {
    padding-top: 15px;
    padding-bottom: 15px;
    margin-left: 20px;
    font-size: 16px;
    border-bottom: 1px solid rgba(187, 187, 187, 0.5);

    &:last-child {
      border-bottom: none;
    }

    .flex-container {
      .title {
        flex: 1 1;
        text-align: left;
        padding-left: 10px;

        a.entry {
          color: #495060;

          &:hover {
            color: #2d8cf0;
            border-bottom: 1px solid #2d8cf0;
          }
        }
      }

      .creator {
        flex: none;
        width: 200px;
        text-align: center;
      }

      .date {
        flex: none;
        width: 200px;
        text-align: center;
      }
    }
  }
}

.content-container {
  padding: 0 20px 20px 20px;
}

.no-announcement {
  text-align: center;
  font-size: 16px;
}

changeLocale
.announcement-animate-enter-active {
  animation: fadeIn 1s;
}
</style>
