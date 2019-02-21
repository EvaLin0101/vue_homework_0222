<template>
  <div class="top_nav">
    <ul>
      <li class="logo" ><img src="./../assets/logo.png" @click="happyNewYear()"></li>
      <li v-for="(item,index) in listItem" :key="index" @click="changeText(index,item)">{{item}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TopNav',
  props: {
    listItem: Array
  },
  methods:{
    changeText(n,content) {
      if(content == 'member'){
        this.listItem.splice(n,1,'helloworld')
      }
      else if(content == 'news'){
        this.listItem.splice(n,1,'happyNews')
      }
    },
    happyNewYear(){
      alert('happy new year!!’')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .top_nav {
    background-color: #333;
    color: #eee;
  }
  .top_nav ul {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .top_nav li {
    padding: 5px;
    flex: 1;
    text-align: center;
  }
  .top_nav .logo {
    text-align-last: left;
  }
  .top_nav img {
    width: 40px;
    margin-left: 10px;
  }
</style>
