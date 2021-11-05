<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="username"
           placeholder="请输入用户名">
    <br>
    <input type="password" v-model="password"
    placeholder="请输入密码" @keyup.enter="login">
    <br>
    <button @click="login">click me!</button>
  </div>
</template>

<script>
// import { Message } from 'element-plus';
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return{
      loginn:false,
      username:'',
      password:''
    }
  },
  methods:{
    login(){
      this.loginn=true
      fetch('http://localhost:8000/login',{
        method:'post',
        headers: {
          'Content-Type': 'application/json'
        },
        body:JSON.stringify({
          username:this.username,
          password:this.password
        })
      }).then(res=>res.json()
      ).then(
          data=> {
            console.log(data)
            if (data.code===200){
                // Message.success({
                //   content:'登录成功',
                //   duration:0.3})
            }
            else{
              // Message.error({
              //   content:'登录失败请重试',
              //   duration:1.0})
            }
          }
      )
      console.log('logging in!')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
input{
  margin-bottom: 20px;
  height: 30px;
  width: 200px;
  text-align: left;
}
.hello{
  align-content: center;
  padding-bottom: 10px;
}
</style>
