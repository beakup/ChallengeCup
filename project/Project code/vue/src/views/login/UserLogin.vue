
<template>
  <div id="login">
    <transition appear name="opacitytrans">
      <div class="container" id="container">
        <div class="form-container sign-in-container">
          <el-form :model="userEdge":rules="rules" ref="loginForm" action="#">
            <h1>乳腺癌预检测系统</h1>
            <span>Version 1.0.0</span>
            <input placeholder="请输入姓名" prefix-icon="el-icon-user" size="medium" v-model="userEdge.name" />

            <input placeholder="请输入密码" show-password prefix-icon="el-icon-lock" size="medium" v-model="userEdge.password" />
            <div class="button" @click="login">登录</div>
            <div class="button" @click="$router.push('/register')">注册</div>
          </el-form>
        </div>
        <div class="overlay-container">
          <div class="overlay">
            <div class="overlay-panel overlay-right">
              <img class="logo" src="@/assets/logo.png" alt="" />
              <p>
                「 Health is everything 」
              </p>
              <!-- <button class="ghost" id="signUp">About Us</button>n -->
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
import request from "@/utils/request";
import Cookies from 'js-cookie';
export default {
  name: 'LOGIN',
  data() {
    return {
      userEdge: {},
      rules: {
        name: [
          {required: true, message: '请输入账号', trigger: 'blur'},
          { min: 3,max: 12,message: '长度为3-12个字符', trigger: 'blur'}
        ],
        password: [
          {required: true, message: '请输入账号密码', trigger: 'blur'},
          { min: 3,max: 12,message: '长度为3-12个字符', trigger: 'blur'}
        ]
      }
    }
  },
  methods: {
    login() {
      this.$refs['loginForm'].validate((valid) => {
        if (valid) {
          request.post('/userEdge/login',this.userEdge).then(res => {
            if(res.code === '200') {
              this.$notify.success("登录成功")
              if (res.data !== null) {
                Cookies.set('userEdge',JSON.stringify(res.data))
              }
              //先存数据再跳转，否则路由守卫会出错
              this.$router.push('/UserLayout')
            } else {
              this.$notify.error(res.msg)
            }
          })
        }
      })
    }
  }
}
</script>

<style  scoped>
#login {
  font-family: "Montserrat", sans-serif;
  background: #f6f5f7;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  /* margin: -20px 0 50px; */
  /* background-image: url("https://www.17sucai.com/preview/1749733/2019-06-22/%E7%99%BB%E5%BD%95/img/img1.png"); */
  background-image: url('https://wallhaven.cc/w/rrpp6m');
  background-size: cover;
}
.logo {
  width: 160px;
  height: auto;
}
h1 {
  font-weight: bold;
  margin: 0;
  color: beige;
}

p {
  font-size: 14px;
  font-weight: bold;
  line-height: 20px;
  letter-spacing: 0.5px;
  margin: 20px 0 30px;
}

span {
  font-size: 12px;
  color: beige;
}

a {
  color: #fff;
  font-size: 14px;
  text-decoration: none;
  margin: 15px 0;
}

.container {
  border-radius: 10px;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  position: absolute;
  overflow: hidden;
  width: 768px;
  max-width: 100%;
  min-height: 480px;
  opacity: 0.8;
}

.form-container form {
  background: rgba(45, 52, 54, 1);
  display: flex;
  flex-direction: column;
  padding: 0 50px;
  height: 100%;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.social-container {
  margin: 20px 0;
}

.social-container a {
  border: 1px solid #ddd;
  border-radius: 50%;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  margin: 0 5px;
  height: 40px;
  width: 40px;
}

.form-container input {
  background: #eee;
  border: none;
  padding: 12px 15px;
  margin: 8px 0;
  width: 100%;
}

.button {
  cursor: pointer;
  border-radius: 20px;
  /* border: 1px solid #ff4b2b;
  background: #ff4b2b; */
  /* border: 1px solid #fa8817;
  background: #fa8817; */
  border: 1px solid #1BBFB4;
  background: #1BBFB4;
  color: #fff;
  font-size: 12px;
  font-weight: bold;
  padding: 12px 45px;
  margin-top: 20px;
  letter-spacing: 1px;
  text-transform: uppercase;
  transition: transform 80ms ease-in;
}

input[type="text"] {
  width: 240px;
  text-align: center;
  background: transparent;
  border: none;
  border-bottom: 1px solid #fff;
  font-family: "PLay", sans-serif;
  font-size: 16px;
  padding: 10px 0;
  transition: border 0.5s;
  outline: none;
  color: #fff;
  font-weight: bold;
}

input[type="password"] {
  width: 240px;
  text-align: center;
  background: transparent;
  border: none;
  border-bottom: 1px solid #fff;
  font-family: "PLay", sans-serif;
  font-size: 16px;
  font-weight: bold;
  padding: 10px 0;
  transition: border 0.5s;
  outline: none;
  color: #fff;
}

input[type="email"] {
  width: 240px;
  text-align: center;
  background: transparent;
  border: none;
  border-bottom: 1px solid #fff;
  font-family: "PLay", sans-serif;
  font-size: 16px;

  padding: 10px 0;
  transition: border 0.5s;
  outline: none;
  color: #fff;
  font-weight: bold;
}

.button:active {
  transform: scale(0.95);
}

.button:focus {
  outline: none;
}

.button.ghost {
  background: transparent;

  /* border-color: #fa8817;
  background-color: #fa8817; */
  border-color: #1BBFB4;
  background-color: #1BBFB4;
  margin: 0;
}

.form-container {
  position: absolute;
  top: 0;
  height: 100%;
  transition: all 0.6s ease-in-out;
}

.sign-in-container {
  left: 0;
  width: 50%;
  z-index: 2;
}

.sign-up-container {
  left: 0;
  width: 50%;
  z-index: 1;
  opacity: 0;
}

.overlay-container {
  position: absolute;
  top: 0;
  left: 50%;
  width: 50%;
  height: 100%;
  overflow: hidden;
  transition: transform 0.6s ease-in-out;
  z-index: 100;
}

.overlay {
  background: transparent;
  background: linear-gradient(to right, #ff4b2b, #ff416c);
  color: #fff;
  position: absolute;
  left: -100%;
  height: 100%;
  width: 200%;
  transform: translateX(0);
  transition: transform 0.6s ease-in-out;
}

.overlay-panel {
  position: absolute;
  top: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0 40px;
  height: 100%;
  width: 50%;
  text-align: center;
  transform: translateX(0);
  transition: transform 0.6s ease-in-out;
}

.overlay-right {
  right: 0;
  transform: translateX(0);
}
</style>

00