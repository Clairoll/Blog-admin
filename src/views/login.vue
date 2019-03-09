<template>
  <div class="login">
    <el-row>
      <el-col :span="8">
        <el-input id="name" v-model="username" placeholder="请输入帐号">
          <template slot="prepend">帐号</template>
        </el-input>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="8">
        <el-input id="password" v-model="password" type="password" placeholder="请输入密码">
          <template slot="prepend">密码</template>
        </el-input>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="8">
        <el-button id="login" v-on:click="login" style="width:100%" type="primary">登录</el-button>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "",
  data() {
    return {
      username: "",
      password: ""
    };
  },
  methods: {
    login() {
      if (this.username == "" || this.password == "") {
        this.$message({
          message: "账号或密码为空！",
          type: "error"
        });
        return;
      } else {
        axios({
          method: "post",
          url: "/api/login",
          data: {
            username: this.username,
            password: this.password
          }
        }).then(res => {
          let user = res.data.user;
          if (user != "") {
            this.$router.push({ path: "/home" });
          } else {
            this.$message({
              message: "账号或密码不对！",
              type: "error"
            });
          }
        });
      }
    }
  }
};
</script>

<style>
.el-row {
  margin-bottom: 20px;
}
.login {
  margin-top: 20%;
  margin-left: 40%;
}

body {
  background: url(../assets/img/bg.jpg) no-repeat;
  background-size: cover;
  font-size: 16px;
}
</style>
