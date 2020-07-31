<template>
  <div class="resource">
    <h2>用户 {{username}} 的资源列表</h2>
    <el-table :data="permissions" style="width: 100%">
      <el-table-column prop="id" label="id"></el-table-column>
      <el-table-column prop="name" label="name"></el-table-column>
      <el-table-column prop="url" label="url"></el-table-column>
      <el-table-column prop="desc" label="描述"></el-table-column>
    </el-table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      permissions: [],
      instance: null,
      username: ''
    };
  },
  created() {
    this.instance = axios.create({
      baseURL: this.GLOBAL.baseURL + "/resource"
    });

    this.instance
      .get("/list")
      .then(result => {
        this.permissions = result.data.data;
      })
      .catch(err => {
        console.log(err);
      });

    axios.get(this.GLOBAL.baseURL + "/user/info").then(result => {
        this.username = result.data.data;
    })
  }
};
</script>