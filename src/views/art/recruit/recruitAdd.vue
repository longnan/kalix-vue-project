<!--
描述：艺术中心-招聘管理-公司招聘-新增组件
开发人：hqj
开发日期：2017年12月18日
-->

<template lang="pug">
  kalix-dialog.user-add(bizKey="artRecruit" ref="kalixBizDialog" v-bind:formModel.sync="formModel" v-bind:targetURL="targetURL")
    div.el-form.kalix-form-table(slot="dialogFormSlot")
      div.table-title 企业信息
      div
        el-form-item.kalix-form-table-td(label="企业组织机构代码" prop="companyCode" v-bind:rules="rules.companyCode" v-bind:label-width="labelWidth")
          template(v-if="isAdmin")
            div.s-flex
              el-input(v-model="formModel.companyCode" placeholder="请输入企业组织机构代码进行查询" v-on:focus="onCompanyCodeFocus")
              el-button(type="primary" icon="el-icon-search" v-on:click="getCompanyByCode") 查询
          template(v-else)
            el-input(v-model="formModel.companyCode" disabled)
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="企业名称" prop="companyName" v-bind:rules="rules.companyName" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyName" disabled)
        el-form-item.s-flex_item.kalix-form-table-td(label="企业邮箱" prop="companyEmail" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyEmail" disabled)
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="固定电话" prop="companyPhone" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyPhone" disabled)
        el-form-item.s-flex_item.kalix-form-table-td(label="手机" prop="companyMobile" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyMobile" disabled)
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="企业性质" prop="companyNature" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.companyNature" appName="art" dictType="企业性质" disabled)
        el-form-item.s-flex_item.kalix-form-table-td(label="企业规模" prop="companyScale" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyScale" disabled)
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="企业行业" prop="companyIndustry" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.companyIndustry" appName="art" dictType="企业行业" disabled)
        el-form-item.s-flex_item.kalix-form-table-td(label="企业年限" prop="companyLife" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyLife" disabled)
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="企业所在省份" prop="companyRegion" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.companyRegion" appName="art" dictType="省份" disabled)
        el-form-item.s-flex_item.kalix-form-table-td(label="企业所在城市" prop="companyCity" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyCity" disabled)
      div
        el-form-item.kalix-form-table-td(label="企业详细地址" prop="companyAddress" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.companyAddress" disabled)
      div.table-title 招聘信息
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="发布时间" prop="publishDate" v-bind:label-width="labelWidth")
          kalix-date-picker.kalix-date(v-model="formModel.publishDate" placeholder="发布时间" readonly)
        el-form-item.s-flex_item.kalix-form-table-td(label="岗位名称" prop="position" v-bind:rules="rules.position" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.position")
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="工作省份" prop="region" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.region" appName="art" dictType="省份")
        el-form-item.s-flex_item.kalix-form-table-td(label="工作城市" prop="city" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.city")
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="岗位要求" prop="positionRequires" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.positionRequires" type="textarea")
        el-form-item.s-flex_item.kalix-form-table-td(label="岗位所需软件" prop="requireSofts" v-bind:label-width="labelWidth")
          el-input(v-model="formModel.requireSofts" type="textarea")
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="岗位个数" prop="jobNumbers" v-bind:label-width="labelWidth")
          el-input-number(v-model="formModel.jobNumbers" v-bind:min="1" style="width:100%")
        el-form-item.s-flex_item.kalix-form-table-td(label="学历" prop="education" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.education" appName="art" dictType="学历")
      div
        el-form-item.kalix-form-table-td(label="职能类别" prop="functionCategoryId" v-bind:label-width="labelWidth")
          kalix-fc-tree2(v-model="formModel.functionCategoryId" v-bind:treeDataURL="functionCategroyURL")
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="实习薪资" prop="probationSalary" v-bind:label-width="labelWidth")
          <!--el-input-number(v-model="formModel.probationSalary" v-bind:step="400" style="width:100%")-->
          kalix-dict-select(v-model="formModel.probationSalary" appName="art" dictType="月薪")
        el-form-item.s-flex_item.kalix-form-table-td(label="转正薪资" prop="salary" v-bind:label-width="labelWidth")
          <!--el-input-number(v-model="formModel.salary" v-bind:step="500" style="width:100%")-->
          kalix-dict-select(v-model="formModel.salary" appName="art" dictType="月薪")
      <!--div-->
        <!--el-form-item.kalix-form-table-td(label="应用技术名称" prop="appliedTechnology" v-bind:label-width="labelWidth")-->
          <!--el-input(v-model="formModel.appliedTechnology" type="textarea")-->
      div.s-flex
        el-form-item.s-flex_item.kalix-form-table-td(label="个人要求" prop="personRequires" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.personRequires" appName="art" dictType="个人要求" multiple placeholder="请选择,可多选")
        el-form-item.s-flex_item.kalix-form-table-td(label="工作类型" prop="jobType" v-bind:label-width="labelWidth")
          kalix-dict-select(v-model="formModel.jobType" appName="art" dictType="工作类型")
</template>

<script type="text/ecmascript-6">
  import FormModel from './model'
  import {RecruitURL, CompanyURL, FunctionCategroyURL} from '../config.toml'
  import Dialog from '@/components/custom/baseDialog.vue'
  import BaseDictSelect from '@/components/custom/baseDictSelect'
  import DatePicker from '@/components/biz/date/datepicker.vue'
  import FcTree2 from '@/components/tree/basetree2'
  import Vue from 'vue'
  import Cache from 'common/cache'

  export default {
    data() {
      return {
        formModel: Object.assign({}, FormModel),
        rules: {
          companyCode: [{required: true, message: '请输入企业组织机构代码', trigger: 'blur'}],
          companyName: [{required: true, message: '请通过代码查询企业名称', trigger: 'blur'}],
          position: [{required: true, message: '请输入岗位名称', trigger: 'blur'}]
        },
        targetURL: RecruitURL,
        labelWidth: '160px',
        functionCategroyURL: FunctionCategroyURL
      }
    },
    components: {
      KalixDialog: Dialog,
      KalixDictSelect: BaseDictSelect,
      KalixDatePicker: DatePicker,
      KalixFcTree2: FcTree2
    },
    mounted() {
      if (!this.isAdmin) {
        this.getCompanyByUserId()
      }
    },
    computed: {
      // 判断当前登录用户是否是管理员
      isAdmin() {
        return (Cache.get('id') * 1 === -1 || Cache.get('id') * 1 === -2)
      }
    },
    methods: {
      onCompanyCodeFocus() {
        this.initData()
      },
      initData() {
        this.formModel.companyName = ''
        this.formModel.companyEmail = ''
        this.formModel.companyPhone = ''
        this.formModel.companyMobile = ''
        this.formModel.companyNature = null
        this.formModel.companyScale = ''
        this.formModel.companyIndustry = null
        this.formModel.companyLife = ''
        this.formModel.companyRegion = null
        this.formModel.companyCity = ''
        this.formModel.companyAddress = ''
      },
      getCompanyByCode() {
        this.initData()
        let companyCode = this.formModel.companyCode
        // let sort = '[{\'property\': \'creationDate\', \'direction\': \'DESC\'}]'
        if (companyCode) {
          let params = {
            params: {
              'jsonStr': {'code': companyCode},
              'page': 1,
              'limit': 1,
              'sort': null
            }
          }
          Vue.axios.get(CompanyURL, params).then((response) => {
            if (response.data.data && response.data.data.length > 0) {
              let rec = response.data.data[0]
              // this.formModel = Object.assign({}, rec)
              this.formModel.companyName = rec.name
              this.formModel.companyEmail = rec.email
              this.formModel.companyPhone = rec.phone
              this.formModel.companyMobile = rec.mobile
              this.formModel.companyNature = rec.nature
              this.formModel.companyScale = rec.scale
              this.formModel.companyIndustry = rec.industry
              this.formModel.companyLife = rec.life
              this.formModel.companyRegion = rec.region
              this.formModel.companyCity = rec.city
              this.formModel.companyAddress = rec.address
            }
          })
        } else {
          alert('请输入企业组织机构代码')
        }
      },
      getCompanyByUserId() {
        this.initData()
        this.formModel.companyCode = ''
        let userId = Cache.get('id')
        // let sort = '[{\'property\': \'creationDate\', \'direction\': \'DESC\'}]'
        if (userId) {
          let params = {
            params: {
              'jsonStr': {'userId': userId},
              'page': 1,
              'limit': 1,
              'sort': null
            }
          }
          Vue.axios.get(CompanyURL, params).then((response) => {
            if (response.data.data && response.data.data.length > 0) {
              let rec = response.data.data[0]
              // this.formModel = Object.assign({}, rec)
              this.formModel.companyCode = rec.code
              this.formModel.companyName = rec.name
              this.formModel.companyEmail = rec.email
              this.formModel.companyPhone = rec.phone
              this.formModel.companyMobile = rec.mobile
              this.formModel.companyNature = rec.nature
              this.formModel.companyScale = rec.scale
              this.formModel.companyIndustry = rec.industry
              this.formModel.companyLife = rec.life
              this.formModel.companyRegion = rec.region
              this.formModel.companyCity = rec.city
              this.formModel.companyAddress = rec.address
            }
          })
        } else {
          alert('请重新登录系统!')
        }
      }
    }
  }
</script>

<style lang="stylus">
  .kalix-date
    .el-input__inner
      background-color: #f5f7fa
</style>
