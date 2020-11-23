<template lang="pug">
div#app
  el-form(:model="formData" :rules="rules" ref="form")
    el-form-item(label='用户名' prop="username")
      el-input(v-model="formData.username")
    el-form-item(label='密码' prop="password")
      el-input(v-model="formData.password" show-password)
    el-form-item
      button(@click="submit") 提交
</template>

<script>
import ElForm from "./components/ElForm.vue";
import ElFormItem from "./components/ElFormItem.vue";
import ElInput from "./components/ElInput.vue";

export default {
  name: "App",
  components: {
    ElForm,
    ElFormItem,
    ElInput
  },
  data() {
    return {
      formData: {},
      rules: {
        username: [
          { required: true, message: "请输入用户名" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符" }
        ],
        password: [
          { required: true, message: "请输入密码" },
          { min: 6, max: 16, message: "长度在 6 到 16 个字符" }
        ]
      }
    };
  },
  methods: {
    submit() {
      this.$refs.form.validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
