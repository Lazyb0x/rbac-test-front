<template>
    <div class="profile">
        <p>你的名字是：{{username}}</p>
    </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      instance: null
    };
  },
  created() {
    this.instance = axios.create({
      baseURL: this.GLOBAL.baseURL + "/user"
    });

    this.instance.get("/info").then(result => {
        this.username = result.data.data;
    }).catch(err => {
        console.log("请求数据失败！");
        console.log(err);
    });
  }
};
</script>