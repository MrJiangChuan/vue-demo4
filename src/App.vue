<template>
  <div id="app">
      <h3>1. Promise基本使用</h3>
      <input type="text" disabled="false" v-model="msg" />
      <input type="button" value="发送定时任务" @click="handler" />
      <hr>
      <h3>2. 基于Promise处理Ajax请求</h3>
      <input type="button" value="发送Ajax请求" @click="handler1" />
  </div>
</template>

<script>


export default {
  name: 'App',
  data: () => {
	  return {
      msg: '冲冲冲'
    }
  },
  methods: {
    handler: () => {
      let p = new Promise((resolve, reject) => {
        let flag = Math.random()//[0,1)
        setTimeout(() => {
          if(flag>=0.5){
            resolve('请求成功')
          }else{
            reject('请求失败')
          }
        },2000)
      })

      p.then((ret) => {
        console.log(ret)

      })
      .catch((error) => {
        console.log(error)
      })
    },
    queryData(url) {
      let p = new Promise(function(resolve, reject){
        let xhr = new XMLHttpRequest()
        xhr.onreadystatechange = function() {
          if(xhr.readyState != 4)return
          if(xhr.readyState == 4 && xhr.status == 200){
            resolve(xhr.responseText)
          }else{
            reject('请求出错')
          }
        }
        xhr.open('GET',url)
        xhr.send(null)
      })
      return p
    },
    handler1() {
      this.queryData('http://localhost:8080/api/user/info/1')
      .then((data) => {
        console.log(data)
      },(error) => {
        console.log(error)
      })
    }
  },
  components: {

  }
}
</script>

<style>
#app {

}
</style>
