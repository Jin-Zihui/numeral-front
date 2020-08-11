<template>
  <div class="home">
    <h1>Welcome to Register Page</h1>
      <h2>用户注册</h2><br>
      <label>用户名</label>
      <input v-model="username" placeholder="请输入用户名"><br><br>
      <label>密码</label>
      <input v-model="password" type="password" placeholder="请输入密码"><br><br>
      <label>再次输入密码</label>
      <input type="password" v-model="rePassword" placeholder="请再次输入密码"><br><br>
      <label>个人简介</label>
      <textarea v-model="selfIntroduction" placeholder="请简单介绍一下自己"></textarea><br><br>
      <button @click="submit" >注册</button>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Register",
  components: {},
  data: function () {
    return {
      username: '',
      password: '',
      rePassword: '',
      selfIntroduction: ''
    };
    
  },
  methods: {
    submit() {
      if(this.username.length === 0) {
        alert("请输入用户名")
      }
      else if(this.password.length < 8) {
        alert("密码长度不足")
      }
      else if (this.password === this.rePassword) {
        let con = confirm("用户名：" + this.username +  ' 个人简介：' + this.selfIntroduction);
        if (con) {
          alert("注册成功");
          this.$router.replace('/');
        }
      }else {
        alert("两次密码输入不一致！")
      }
    }
  },
  created() {
    // 测试基础通信能否建立
    this.axios
      .post("/api/users", { username: "asd", password: "asdsad", description: "20 years old" })
      .then((res) => {
        console.log(res);
      })
      .catch((err) => {
        console.error(err);
      });
  },
};
</script>
