<!--
描述：办公自动化-流程定义查看管理组件
开发人：sunlf
开发日期：2017年8月17日
-->
<template lang="pug">
  div
    kalix-dialog(v-bind:title="title" v-bind:visible="visible" ref="kalixBizDialog"
    v-bind:close-on-click-modal="false" v-bind:formModel="formModel" v-bind:isView="isView")
      div(slot="dialogFormSlot")
        img(v-bind:src="imgUrl" style="width:100%")
</template>

<script type="text/ecmascript-6">
  import {ON_INIT_DIALOG_DATA} from '@/components/custom/event.toml'
  import {baseURL} from 'config/global.toml'
  import EventBus from 'common/eventbus'
  import Dialog from '@/components/custom/baseDialog.vue'

  const viewURL = baseURL + `/image?processDefinitionId=`
  export default {
    data() {
      return {
        bizKey: 'processDefinition',
        title: '',
        visible: false,
        isView: true,
        imgUrl: '',
        formModel: {}
      }
    },
    mounted() {
//      console.log('mounted', this.bizKey + '-' + ON_INIT_DIALOG_DATA)
      EventBus.$on(this.bizKey + '-' + ON_INIT_DIALOG_DATA, this.initData)
    },
    components: {
      KalixDialog: Dialog
    },
    methods: {
      initData(row) {
        this.title = '流程定义查看-' + row.name
        this.imgUrl = viewURL + row.id
      }
    }
  }
</script>

<style scoped lang="stylus">

</style>
