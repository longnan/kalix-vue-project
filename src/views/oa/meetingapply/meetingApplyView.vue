<!--
描述：人员管理-会议申请-查看组件
开发人：sunlf
开发日期：2017年8月17日
-->

<template lang="pug">
  kalix-dialog.user-add(bizKey="meetapply"
  v-bind:formModel.sync="formModel" v-bind:targetURL="targetURL"
  ref="kalixBizDialog"
  v-bind:isView="readonly"
  )
    div.el-form.kalix-form-table-view(slot="dialogFormSlot")
      kalix-meeting-apply-view-form(v-bind:form-model="formModel")
</template>

<script type="text/ecmascript-6">
  import Dialog from '@/components/custom/baseDialog.vue'
  import BaseDictSelect from '@/components/custom/baseDictSelect'
  import UserSelect from '@/components/biz/userselect/userselect'
  import MeetingApplyViewForm from './MeetingApplyViewForm'
  import FormModel from './model'

  export default {
    data() {
      return {
        formModel: Object.assign({}, FormModel),
        targetURL: '',
        readonly: true,
        meetingTypeName: ''
      }
    },
    created() {
      this.labelWidth = '110px'
      console.log('[meetingApplyView.vue created] this.formModel:', this.formModel)
      console.log('[meetingApplyView.vue created] this.formModel.meetingType', this.formModel.meetingType)
//      this.getMeetingTypeName()
    },
    components: {
      KalixDialog: Dialog,
      KalixDictSelect: BaseDictSelect,
      KalixMeetingApplyViewForm: MeetingApplyViewForm,
      KalixUserSelect: UserSelect
    },
    methods: {}
  }
</script>
