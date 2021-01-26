<template>
  <div class="header">
    <div class="title">MyBlog</div>
    <div class="login-box">
      <div v-if="isExist==0">
         <a href="/login">登录</a> | <a href="/regist">注册</a>
    </div>
      <div v-else>{{ loginUser }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginUser: '',
      isExist:0
    };
  },
  created() {
    this.getloginUser();
  },
  methods: {
    getloginUser() {
      if (localStorage.getItem("user")) {
        this.loginUser = localStorage.getItem("user");
        console.log(this.loginUser);
        this.isExist=1;
      }
    },
  },
};
</script>

<style  scoped>
.header {
  height: 50px;
  background: #c0e4eb;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgb(112, 152, 238);
}
</style>