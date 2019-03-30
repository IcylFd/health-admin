<template>
  <div>
    <Form ref="formItem" :model="formItem" :rules="ruleValidate" :label-width="400">
        <FormItem label="姓名" prop="name">
            <Input v-model="formItem.name" placeholder="请输入姓名..."></Input>
        </FormItem>
        <FormItem label="性别">
            <RadioGroup v-model="formItem.sex">
                <Radio label="男"></Radio>
                <Radio label="女"></Radio>
            </RadioGroup>
        </FormItem>
        <FormItem label="出生日期">
          <DatePicker value='1998-01-01' type="date" placeholder="请选择日期"  v-model="formItem.birthday"></DatePicker>
        </FormItem>
        <FormItem label="邮箱" prop="mail" error>
            <Input v-model="formItem.mail" placeholder="请输入电子邮箱..."></Input>
        </FormItem>
        <FormItem label="电话" prop="phone">
            <Input v-model="formItem.phone" placeholder="请输入电话..."></Input>
        </FormItem>
        <FormItem label="部门" prop="department">
            <Select v-model="formItem.department">
                <Option value="技术部"></Option>
                <Option value="法务部"></Option>
                <Option value="人事部"></Option>
            </Select>
        </FormItem>
        <FormItem label="是否为超级管理员">
            <i-switch v-model="formItem.isSuperAd" size="large">
                <span slot="open">是</span>
                <span slot="close">否</span>
            </i-switch>
        </FormItem>
        <FormItem label="备注">
            <Input
                v-model="formItem.ps_msg"
                type="textarea"
                :autosize="{minRows: 2,maxRows: 5}"
            ></Input>
        </FormItem>
        <FormItem>
            <Button type="primary" @click="handleCommitFirst('formItem')">提交</Button>
            <Button style="margin-left: 8px" @click="handleClear('formItem')">清空</Button>
        </FormItem>
    </Form>
    <Modal
      v-model="confirm_modal "
      title="请确认提交信息"
      @on-ok="handleCommit()"
      @on-cancel="cancel">
      <p class="is-superad" style="color:#2d8cf0; font-size:14px; margin-bottom: 5px">
        <span v-if='formItem.isSuperAd'>超级管理员</span>
        <span v-else>普通管理员</span>
      </p>
      <p style="display:inline">姓名：{{formItem.name}}</p>
      <p>性别：{{formItem.sex}}</p>
      <p>出生日期：{{formItem.birthdayStr}}</p>
      <p>邮箱：{{formItem.mail}}</p>
      <p>电话：{{formItem.phone}}</p>
      <p>部门：{{formItem.department}}</p>
      <p v-if='formItem.ps_msg'>备注：{{formItem.ps_msg}}</p>
    </Modal>
  </div>
</template>
<script>
export default {
  data() {
    return {
      confirm_modal: false,
      birthdayValue: '1998-01-01',
      formItem: {
        name: "",
        sex: "男",
        mail: "",
        phone: "",
        department: "",
        isSuperAd: false,
        birthday: new Date(),
        birthdayStr: "",
        ps_msg: ""
      },
      ruleValidate: {
        name: [
            { required: true, message: '姓名不能为空', trigger: 'blur'}
        ],
        mail: [
            { required: true, message: '电子邮箱不能为空', trigger: 'blur' },
            { type: 'email', message: '电子邮箱格式不正确', trigger: 'blur' }
        ],
        phone: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
        ],
        department: [
            { required: true, message: '请选择部门', trigger: 'blur' }
        ],
      }
    }
  },
  methods: {
    handleClear (name) {
      this.$refs[name].resetFields();
    },
    handleCommitFirst(name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
            this.formItem.birthdayStr = this.formatDate(this.formItem.birthday);
            this.confirm_modal = true;
        } else {
            this.$Message.config({
              top: 200
            })
            this.$Message.error('表单验证失败');
        }
      })
      
    },
    handleCommit () {
      this.$router.push({
        name: 'admin_page',
        params: this.formItem
      })
    },
    cancel () {

    },
    formatDate(date) {
      var year = date.getFullYear();
      var month = date.getMonth() + 1;
      var day = date.getDate();
      return year + '-' + month + '-' + day;
    }
  },
}
</script>

<style lang="less" scoped>
  .ivu-form{
    margin: 0 auto;
    .ivu-input-wrapper,
    .ivu-select{
      width: 50%;
    }
  }
</style>

