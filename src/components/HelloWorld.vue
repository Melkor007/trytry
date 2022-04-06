<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="question"
           placeholder="请输入问题" @keyup.enter="qa()">
    <br>
      <textarea cols="100" rows="10" v-model="answer"></textarea>
    <br>
    <el-button type="primary" @click="qa()">Click me</el-button>
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
      question:'请输入您的问题',
      answer:'答案会显示在这里'
    }
  },
  methods:{
    testo(){
      fetch('http://127.0.0.1:8888/test'
      ).then(function(res){
        console.log(res)
        this.answer = res
      })
    },
    qa(){
      this.loginn=true
      fetch('http://localhost:8888/kbqa',{
        method:'post',
        headers: {
          'Content-Type': 'application/json'
        },
        body:JSON.stringify({
          question:this.question,
        })
      }).then(res=>res.json()
      ).then(
          data=> {
            console.log(data)
            this.answer = 'neo4j查询结果：'+data.answer
            let entity = data.entity
            let mention = data.mention
            let intention = data.intention
            this.answer += '\n实体识别：'+mention
            this.answer += '\n实体链接：'+entity
            this.answer += '\n意图识别：'+intention
            if (data.code===200){
                this.$message.success('success')
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
