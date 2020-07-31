<template>
  <div class="login">
    <h1>登录</h1>
    <el-row>
      <el-col :span="8">
        <div class="grid-content"></div>
      </el-col>
      <el-col :span="8">
        <div>
          <el-form class="el-form" label-width="80px" :model="user">
            <el-form-item label="用户名">
              <el-input v-model="user.name"></el-input>
            </el-form-item>
            <el-form-item label="密码">
              <el-input v-model="user.password"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="onSubmit">提交</el-button>
            </el-form-item>
          </el-form>
        </div>
      </el-col>
    </el-row>

    <el-button plain @click="open1">测试</el-button>
  </div>
</template>

<style>
/* .el-form {
  width: 460px;
  margin: 0 auto;
} */
.grid-content {
  min-height: 15px;
}
</style>


<script>
import axios from "axios";

export default {
  data() {
    return {
      user: {
        name: "",
        password: ""
      },
      instance: null
    };
  },
  created() {
    this.instance = axios.create({
      baseURL: this.GLOBAL.baseURL + "/user"
    });
  },
  methods: {
    open1() {
      this.$notify({
        title: "成功",
        message: "这是一条成功的提示消息",
        type: "success"
      });
    },
    onSubmit() {
      console.log("提交");
      this.instance({
        url: "/login",
        method: "post",
        data: this.user
      })
        .then(res => {
          if (res.data.code == 1) {
            window.location.href = "/profile";
          } else {
            this.$notify.error({
              title: "错误",
              message: "登录失败！"
            });
          }
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>