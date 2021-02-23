<template>
  <Panel shadow :padding="10">
    <div slot="title">
      {{ title }}
    </div>
    <template>
      <ol class="announcements-container" key="list">
        <li v-for="member in members" :key="member.user.username">
          <div class="flex-container">
            <div class="title">
              <a class="entry" @click="goToProfile(member.user.username)">{{ member.user.username }}</a> - {{member.submission_number}} {{submissionTitle}}
            </div>
          </div>
        </li>
      </ol>
    </template>
  </Panel>
</template>

<script>
import api from '@oj/api'

export default {
  name: 'PositiveMember',
  components: {},
  props: {
    limit: {
      type: Number,
      default: 10
    }
  },
  data () {
    return {
      members: []
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {
      this.getPositiveMembers(this.limit)
    },
    getPositiveMembers (limit) {
      api.fetchPositiveMembers(limit).then(res => {
        this.members = res.data.data.members
      }, () => {
      })
    },
    goToProfile (username) {
      this.$router.push({
        name: 'problem-details',
        query: {username: username}
      })
    }
  },
  computed: {
    title () {
      return this.$i18n.t('m.Top_Positive_Members')
    },
    submissionTitle () {
      return this.$i18n.t('m.Submission_Plural')
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
