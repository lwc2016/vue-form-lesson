<template>
  <div id="app">
      <el-form :model="form" :rules="rules" ref="form">
          <el-form-item label="用户名" prop="username">
              <el-input v-model="form.username" placeholder="请填写用户名" />
          </el-form-item>
          <el-form-item label="密码" prop="password">
              <el-input v-model="form.password" placeholder="请填写密码" type="password" />
          </el-form-item>
          <el-form-item>
              <button class="button" @click="handleSubmit">提交</button>
          </el-form-item>
      </el-form>

  </div>
</template>

<script>
import elInput from "./components/el-input";
import elFormItem from "./components/el-form-item";
import elForm from "./components/el-form";

export default {
  name: 'app',
  components: {
    "el-input": elInput,
    "el-form-item": elFormItem,
    "el-form": elForm
  },
  data(){
    return {
      message: "Hello world",
      form: {
        username: "",
        password: ""
      },
      rules: {
        username: [
            {required: true, message: "请填写用户名！"}
        ],
        password: [
            {required: true, message: "请填写密码！"}
        ]
      }
    }
  },
  methods: {
      handleSubmit(){
          this.$refs["form"].validate((err) => {
              console.log(err);
          });
      }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px;
}

    .button{
        width: 60px;
        height: 30px;
        border-radius: 4px;
        outline: none;
        background-color: cornflowerblue;
        color: #ffffff;
        border: none;
        font-size: 16px;
        cursor: pointer;
    }
</style>
