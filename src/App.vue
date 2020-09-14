<template>
  <div id="app">
      <input type="text" disabled="true" v-model="msg" />
      <input type="button" value="发送请求" @click="handler" />
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
