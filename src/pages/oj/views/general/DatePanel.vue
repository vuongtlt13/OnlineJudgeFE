<template>
  <Panel shadow :padding-bottom="10">
    <template v-slot:title>
      <div class="text-center" style="width: 100%">
        <span style="font-size: small">Rủ bạn bè vào cày rank thôi nào!</span>
      </div>
    </template>
    <h1 style="width: 100%" class="text-center">{{dayInWeek}}</h1>
    <h1 style="width: 100%" class="text-center">{{todayInDate}}</h1>
    <div class="ivu-card-head">
      <div class="panel-title text-center">
        <span style="font-size: small">- No pain, no gain -</span>
      </div>
    </div>
  </Panel>
</template>

<script>
  import moment from 'moment'

  export default {
    name: 'DatePanel',
    components: {},
    data () {
      return {
        todayInDate: moment().format('DD/MM/YYYY'),
        dayInWeek: moment().format('dddd'),
      }
    },
    mounted () {
      this.init()
    },
    methods: {
      init () {
      }
    },
    computed: {
    }
  }
</script>

<style scoped>
  .text-center {
    text-align: center;
  }
</style>
