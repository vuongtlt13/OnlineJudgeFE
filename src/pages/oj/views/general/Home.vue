<template>
  <Row type="flex" justify="space-around">
    <Col :span="22">
      <panel shadow v-if="contests.length" class="contest">
        <div slot="title">
          <Button type="text" class="contest-title" @click="goContest">{{ contests[index].title }}</Button>
        </div>
        <Carousel v-model="index" trigger="hover" autoplay :autoplay-speed="6000" class="contest">
          <CarouselItem v-for="(contest, index) of contests" :key="index">
            <div class="contest-content">
              <div class="contest-content-tags">
                <Button type="info" shape="circle" size="small" icon="calendar">
                  {{ contest.start_time | localtime('YYYY-M-D HH:mm') }}
                </Button>
                <Button type="success" shape="circle" size="small" icon="android-time">
                  {{ getDuration(contest.start_time, contest.end_time) }}
                </Button>
                <Button type="warning" shape="circle" size="small" icon="trophy">
                  {{ contest.rule_type }}
                </Button>
              </div>
              <div class="contest-content-description">
                <blockquote v-html="contest.description"></blockquote>
              </div>
            </div>
          </CarouselItem>
        </Carousel>
      </panel>
      <Row type="flex" justify="space-around">
        <Col :span="16">
          <Row>
            <Col :span="24">
              <Announcements class="announcement"></Announcements>
            </Col>
          </Row>

          <Row>
            <Col :span="12">
              <NewProblem :limit="15" class="announcement"></NewProblem>
            </Col>
          </Row>
        </Col>
        <Col :span="6">
          <Row>
            <Col :span="24">
              <DatePanel class="announcement"></DatePanel>
            </Col>

            <Col :span="24">
              <PositiveMember class="announcement"></PositiveMember>
            </Col>
          </Row>
        </Col>
      </Row>
    </Col>
  </Row>
</template>

<script>
import Announcements from './Announcements.vue'
import api from '@oj/api'
import time from '@/utils/time'
import {CONTEST_STATUS} from '@/utils/constants'
import DatePanel from './DatePanel'
import NewProblem from './NewProblem'
import PositiveMember from './PositiveMember'

export default {
  name: 'home',
  components: {
    PositiveMember,
    Announcements,
    DatePanel,
    NewProblem
  },
  data () {
    return {
      contests: [],
      index: 0
    }
  },
  mounted () {
    let params = {status: CONTEST_STATUS.NOT_START}
    api.getContestList(0, 5, params).then(res => {
      this.contests = res.data.data.results
    })
  },
  methods: {
    getDuration (startTime, endTime) {
      return time.duration(startTime, endTime)
    },
    goContest () {
      this.$router.push({
        name: 'contest-details',
        params: {contestID: this.contests[this.index].id}
      })
    }
  }
}
</script>

<style lang="less" scoped>
.contest {
  &-title {
    font-style: italic;
    font-size: 21px;
  }

  &-content {
    padding: 0 70px 40px 70px;

    &-description {
      margin-top: 25px;
    }
  }
}

.announcement {
  margin-top: 20px;
}
</style>
