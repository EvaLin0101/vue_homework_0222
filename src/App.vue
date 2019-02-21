<template>
  <div id="app">
    <header>
      <TopNav :listItem="listItems"/>
      <Slide :slideList="slideItems"/>
      <TodoList/>
    </header>
  </div>
</template>

<script>
import TopNav from './components/TopNav.vue'
import Slide from './components/Slide.vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'app',
  components: {
    TopNav,
    Slide,
    TodoList
  },
  mounted: function () {
    alert('Mounted!')
  },
  data: function () {
    return {
      listItems: ['movie','article','news','member'],
      slideItems: ['banner1','banner2']
    }
  }
}
</script>

<style>
body,html,ul,li {
  padding: 0;
  margin: 0;
}
li {
  list-style: none;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}
button {
  background-color: #666;
  color: #ffffff;
  padding: 5px 8px;
  border: none;
  border-radius: 3px;
  margin: 3px;
}
button.green {
  background-color: #16716c;
}
</style>
