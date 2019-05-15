<template>
  <div id="app">
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
          :checked="clean.checkAll">
          全部
        </a-checkbox>
        <a-checkbox-group v-decorator="['groupClean', {initialValue: formData.groupClean, rules: [{ required: clean.cleanBtn, message: '请选择清洗字段' }]}]" @change="cleanChange">
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
        groupClean: [1]
      },
      clean: {
        cleanBtn: true,
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
    cleanChange () {
      const checkedList = this.form.getFieldValue('groupClean')
      // 获取旧值问题
      console.log(this.form.getFieldValue('groupClean'))
      this.clean.indeterminate = !!checkedList.length && (checkedList.length < this.cleanLists.length - 1)
      this.clean.checkAll = checkedList.length === this.cleanLists.length - 1
    }
  }
}
</script>

<style lang="scss">
#app {
  margin: 40px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
