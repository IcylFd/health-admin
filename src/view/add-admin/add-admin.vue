<template>
    <Form :model="formItem" :rules="ruleValidate" :label-width="400">
        <FormItem label="姓名" prop="name">
            <Input v-model="formItem.name" placeholder="请输入姓名..."></Input>
        </FormItem>
        <FormItem label="性别">
            <RadioGroup v-model="formItem.sex">
                <Radio label="male">男</Radio>
                <Radio label="female">女</Radio>
            </RadioGroup>
        </FormItem>
        <FormItem label="出生日期">
          <DatePicker type="date" placeholder="请选择日期" v-model="formItem.birthday"></DatePicker>
        </FormItem>
        <FormItem label="邮箱" prop="mail">
            <Input v-model="formItem.mail" placeholder="请输入电子邮箱..."></Input>
        </FormItem>
        <FormItem label="电话" prop="phone">
            <Input v-model="formItem.phone" placeholder="请输入电话..."></Input>
        </FormItem>
        <FormItem label="部门" prop="department">
            <Select v-model="formItem.department">
                <Option value="tec">技术部</Option>
                <Option value="law">法务部</Option>
                <Option value="hr">人事部</Option>
            </Select>
        </FormItem>
        <FormItem label="是否为超级管理员">
            <i-switch v-model="formItem.switch" size="large">
                <span slot="open">是</span>
                <span slot="close">否</span>
            </i-switch>
        </FormItem>
        <FormItem label="备注">
            <Input
                v-model="formItem.textarea"
                type="textarea"
                :autosize="{minRows: 2,maxRows: 5}"
            ></Input>
        </FormItem>
        <FormItem>
            <Button type="primary">提交</Button>
            <Button style="margin-left: 8px" @click="handleClear(formItem)">清空</Button>
        </FormItem>
    </Form>
</template>
<script>
export default {
  data() {
    return {
      formItem: {
        name: "",
        sex: "male",
        mail: "",
        phone: "",
        department: "",
        switch: false,
        birthday: "",
        textarea: ""
      },
      ruleValidate: {
        name: [
            { required: true, message: '姓名不能为空', trigger: 'blur' }
        ],
        mail: [
            { required: true, message: '电子邮箱不能为空', trigger: 'blur' },
            { type: 'email', message: '电子邮箱格式不正确', trigger: 'blur' }
        ],
        phone: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
        ],
        department: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
        ],
      }
    }
  },
  methods: {
    handleClear (formItem) {
      formItem.name = "";
      formItem.sex = "male";
      formItem.mail = "";
      formItem.phone = "";
      formItem.department =  "";
      formItem.switch = false;
      formItem.birthday = "";
      formItem.textarea = "";
    }
  }
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

