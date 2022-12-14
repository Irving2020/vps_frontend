<template>
  <div class="Login-box">
    <div class="Login-container">
      <form class="Login-clock" style="color:skyblue">
        <FliqloCo style="z-index:999"/>
      </form>
      <form class="Login-form">
        <h3>LOGIN</h3>
        <h4 style="color:skyblue">Irving blog is coming online ...</h4>
        <el-form
          ref="ruleFormRef"
          :model="ruleForm"
          status-icon
          :rules="rules"
          label-width="120px"
          class="demo-ruleForm"
        >
          <el-form-item label="Password" prop="pass">
            <el-input v-model="ruleForm.pass" type="password" autocomplete="off" />
          </el-form-item>
          <el-form-item label="Confirm" prop="checkPass">
            <el-input
              v-model="ruleForm.checkPass"
              type="password"
              autocomplete="off"
            />
          </el-form-item>
          <el-form-item label="Age" prop="age">
            <el-input v-model.number="ruleForm.age" />
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm(ruleFormRef)"
              >Submit</el-button
            >
            <el-button @click="resetForm(ruleFormRef)">Reset</el-button>
          </el-form-item>
        </el-form>
      </form>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import type { FormInstance } from 'element-plus'
import { defineComponent } from 'vue';
import FliqloCo from './Fliqlo.vue'
const LoginCom = defineComponent({
  // 组件定义
  props:{
    message: String
  },
  setup(props) {
    return {
    }
  },
  components:{
    FliqloCo
  }
})

const ruleFormRef = ref<FormInstance>()

const checkAge = (rule: any, value: any, callback: any) => {
  if (!value) {
    return callback(new Error('Please input the age'))
  } 
  setTimeout(() => {
    if (!Number.isInteger(value)) {
      callback(new Error('Please input digits'))
    } else {
      if (value < 18) {
        callback(new Error('Age must be greater than 18'))
      } else {
        callback()
      }
    }
  }, 1000)
}
const validatePass = (rule: any, value: any, callback: any) => {
  if (value === '') {
    callback(new Error('Please input the password'))
  } else {
    if (ruleForm.checkPass !== '') {
      if (!ruleFormRef.value) return
      ruleFormRef.value.validateField('checkPass', () => null)
    }
    callback()
  }
}

const validatePass2 = (rule: any, value: any, callback: any) => {
  if (value === '') {
    callback(new Error('Please input the password again'))
  } else if (value !== ruleForm.pass) {
    callback(new Error("Two inputs don't match!"))
  } else {
    callback()
  }
}

const ruleForm = reactive({
  pass: '',
  checkPass: '',
  age: '',
})

const rules = reactive({
  pass: [{ validator: validatePass, trigger: 'blur' }],
  checkPass: [{ validator: validatePass2, trigger: 'blur' }],
  age: [{ validator: checkAge, trigger: 'blur' }],
})

const submitForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.validate((valid) => {
    if (valid) {
      console.log('submit!')
    } else {
      console.log('error submit!')
      return false
    }
  })
}

const resetForm = (formEl: FormInstance | undefined) => {
  // if (!formEl) return
  // formEl.resetFields()
}

defineExpose({
  LoginCom
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Login-box{
  width: 100%;
  height: 100vh;
}
.Login-container{
  width: 100%;
  height: 100%;
  margin: auto;
  /* background: url('@/assets/imgs/preview.jpg') 50% 50% no-repeat;
  background-size: cover; */
  background-color: #a093cd;
}
.Login-clock{
  width: 40%;
  height: 20%;
  margin: auto;
  border-radius: 67px;
  text-align: center;
  line-height: 20vh;
  font-family: Arial, Helvetica, sans-serif;
  background: #b5abd8;
  box-shadow: 35px 35px 70px #5e5779,
  -35px -35px 70px #e2cfff;
}
.Login-form{
  width: 50%;
  height: 50%;
  margin: 5% auto;
  border-radius: 28px;
  background: linear-gradient(225deg, #3a3256, #312a48);
  box-shadow:  -32px 32px 64px #161320,
  32px -32px 64px #564b80;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
