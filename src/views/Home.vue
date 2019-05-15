<template>
  <div class="home">
    <a-form :form="form">
      <a-form-item
        :label-col="{ span: 3 }"
        :wrapper-col="{ span: 20 }">
        <span slot="label">
          清洗字段&nbsp;
          <a-tooltip title="线索中必须包含的字段，若某一字段的值未填写、格式错误或语意非法，则线索无效，自动进入归档列表">
            <a-icon type="question-circle-o" />
          </a-tooltip>
        </span>
        <a-checkbox
          :indeterminate="clean.indeterminate"
          @change="onCheckAllChangeClean"
          :checked="clean.checkAll">
          全部
        </a-checkbox>
        <a-checkbox-group v-decorator="['groupClean', {rules: [{ required: clean.cleanBtn, message: '请选择清洗字段' }]}]" @change="cleanChange">
          <a-checkbox class="group-box" v-for="(item, index) in cleanLists" :value="item.id" :key="index">{{item.name}}</a-checkbox>
        </a-checkbox-group>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      form: this.$form.createForm(this),
      formData: {
        groupClean: []
      },
      clean: {
        cleanBtn: false,
        checkAll: false,
        indeterminate: false
      },
      cleanLists: [
        {
          id: 1,
          name: '姓名'
        }, {
          id: 2,
          name: '性别'
        }, {
          id: 3,
          name: '手机号'
        }, {
          id: 4,
          name: '邮箱'
        }
      ]
    }
  },
  methods: {
    onCheckAllChangeClean () {},
    cleanChange () {
      // const checkedList = this.form.getFieldValue('groupClean')
      console.log(this.form.getFieldValue('groupClean'))
      // this.clean.indeterminate = !!checkedList.length && (checkedList.length < this.cleanLists.length - 1)
      // this.clean.checkAll = checkedList.length === this.cleanLists.length - 1
    }
  }
}
</script>
