<template>
  <div class="login-wrap">
    <el-form label-position="top" label-width="80px" :model="formdata" class="login-form">
      <h2>用户登录</h2>
      <el-form-item label="用户名">
        <el-input v-model="formdata.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formdata.password"></el-input>
      </el-form-item>
      <el-row>
        <el-button type="primary" class="login-btn" @click.prevent="">登录</el-button>
      </el-row>
    </el-form>
  </div>
</template>


  <script>
export default {
  data() {
    return {
      formdata: {
        username: "",
        password: ""
      }
    };
  },
  methods:{
      async handleLogin(){
          const res = await this.$http.post("login",this.formdata)
          console.log(res) //查看数据
          const {data,meta:{msg,status}} =res.data
          if(status === 200){
              localStorage.setItem("token",data.token)
              localStorage.setItem("uname",data.username)
              this.$router.push({name:"home"})
              this.$message.success(msg)
          }else{
              this.$message.error(msg)
          }
      }
  }
  
};
</script>

<style>
.login-wrap {
  height: 100%;
  background-color: #324152;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-wrap .login-form {
  width: 400px;
  /* background-color: #fff; */
  padding: 30px;
  border-radius: 5px;
}
.login-wrap .login-btn {
  margin-top: 35px;
  width: 100%;
  border-radius:30px;
}
.login-wrap input {
  border-radius: 30px;
}
.login-wrap label {
  color: aliceblue;
}
</style>