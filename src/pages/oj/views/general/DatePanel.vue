<template>
  <Panel shadow :padding-bottom="10">
    <h1 style="width: 100%" class="text-center">{{todayInDate}}</h1>
    <div class="ivu-card-head"><div class="panel-title"></div></div>
  </Panel>
</template>

<script>
  import moment from 'moment'

  export default {
    name: 'DatePanel',
    components: {},
    data () {
      return {
        todayInDate: moment().format('DD/MM/YYYY')
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
