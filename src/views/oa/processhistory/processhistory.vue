<!--
描述：办公自动化-我的流程组件
开发人：sunlf
开发日期：2017年8月17日
-->

<template lang="pug">
  div
    keep-alive
      base-table(:isShowToolBar="isShowToolBar" bizKey="processhistory" title='流程历史列表'
      v-bind:targetURL="targetURL"
      v-bind:formModel.sync="formModel"
      v-bind:bizDialog="bizDialog"
      v-bind:toolbarBtnList="toolbarBtnList"
      v-bind:isFixedColumn="isFixedColumn"
      bizSearch="OaProcessHistorySearch"
      v-bind:tableRowClassName="tableRowClassName"
      v-bind:customTableTool='customTableTool'
      v-bind:btnList="btnList")
        template(slot="tableColumnSlot")
          kalix-biz-no-column(name="name")
          el-table-column(prop="title" label="业务名称" width="280" align="center")
          el-table-column(prop="startUserId" label="启动用户" align="center")
          kalix-date-column(prop="startTime" label="开始时间")
          kalix-date-column(prop="endTime" label="结束时间")
          el-table-column(prop="durationInMillis" label="持续时长" align="center")
          el-table-column(prop="status" label="状态" align="center")
            template(slot-scope="scope")
              el-tag(:type="scope.row.status | statusFilter") {{scope.row.status}}
              <!--span(style="color:#f00" v-if="scope.row.status === '结束'") {{ scope.row.status }}-->
              <!--span(v-else) {{ scope.row.status }}-->
    kalix-task-complete(ref="kalixTaskDialog" v-bind:isApproveShow="isApproveShow")
</template>

<script type="text/ecmascript-6">
  import BaseTable from '@/components/custom/baseTable'
  import {WorkflowHistoryURL, WorkflowButtonList} from '../config.toml'
  import {registerComp} from 'views/oa/comp'
  import BizNoColumn from 'views/oa/comp/bizNoColumn'
  import DateColumn from 'views/oa/comp/dateColumn'
  import TaskComplete from '@/views/oa/comp/taskComplete'

  export default {
    activated() {
      console.log(this.bizKey + '  is activated')
    },
    deactivated() {
      console.log(this.bizKey + '  is deactivated')
    },
    data() {
      return {
        isFixedColumn: true,
        isApproveShow: false,
        isShowToolBar: false,  // 不显示工具栏
        toolbarBtnList: [{id: 'add', isShow: false}],
        btnList: WorkflowButtonList,
        targetURL: WorkflowHistoryURL,
        bizDialog: [
          {id: 'viewHistory', dialog: ''}
        ],
        formModel: {}
      }
    },
    created() {
//      this.tempFormModel = JSON.stringify(Object.assign({}, this.formModel))
    },
    mounted() {
      registerComp()
    },
    filters: {
      statusFilter(status) {
        const statusMap = {
          已结束: 'success',
          进行中: 'gray',
          已停止: 'danger'
        }
        return statusMap[status]
      }
    },
    methods: {
      tableRowClassName(row, index) {
        if (row.status === '已结束') {
          return 'finish-row'
        }
        return ''
      },
      customTableTool(row, btnId) {
        switch (btnId) {
          case 'viewHistory': {
            this.$refs.kalixTaskDialog.open(row)
            break
          }
        }
      }
    },
    components: {
      BaseTable,
      KalixBizNoColumn: BizNoColumn,
      KalixDateColumn: DateColumn,
      KalixTaskComplete: TaskComplete
//      KalixUserAdd: UserAdd
    }
  }
</script>

<style lang="stylus">
  .el-table
    .finish-row
      td
        background-color #c9e5f5 !important
</style>
