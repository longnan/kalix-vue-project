<!--
描述：办公自动化-流程分类-新增组件
开发人：sunlf
开发日期：2017年8月17日
-->

<template lang="pug">
  kalix-dialog.user-add(bizKey="category"
  ref="kalixBizDialog" v-bind:form-model="formModel" isView
  )
    div.el-form(slot="dialogFormSlot")
      el-form-item(label="分类名称" prop="name")
        el-input(v-model="formModel.name" readonly)
      el-form-item(label="分类主键" prop="key")
        el-input(v-model="formModel.key" readonly)
      el-form-item(label="分类图标" prop="icon")
        el-input(v-model="formModel.icon" readonly)
      el-form-item(label="分类描述" prop="description")
        el-input(v-model="formModel.description" readonly)
</template>

<script type="text/ecmascript-6">
  import Dialog from '@/components/custom/baseDialog.vue'

  export default {
    props: {
      formModel: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
      }
    },
    created() {
    },
    components: {
      KalixDialog: Dialog
    },
    methods: {}
  }
</script>

