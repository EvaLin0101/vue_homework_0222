<template>
  <div class="todoList">
    <div class="functionBtn">
      <button @click="addTodoList" class="green">新增</button>
      <button @click="delCompleteTodoList">刪除完成項目</button>
    </div>
    <p v-if="todoList.length == 0">目前沒有任何待辦事項</p>
    <transition-group name="list-complete" tag="ul">
      <li v-for="(item,index) in todoList" :key="index" class="list-complete-item">
        <span v-if="item.status == 0">
          <span @click="completeTodoList(index,item)" class="checkbox"></span> {{item.text}}
        </span>
        <span v-if="item.status == 1" class="complete">
          <span class="checkbox checked"></span>{{item.text}}
        </span>
        <span v-if="item.status == 2">
          <span class="checkbox disabled"></span><input type="text" v-model="item.text"/>
        </span>
        <button v-if="item.status == 0" @click="editTodoList(index)">修改</button>
        <button v-if="item.status == 0" @click="removeTodoList(index)">刪除</button>
        <button v-if="item.status == 2" @click="saveTodoList(index)" class="green">儲存</button>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data: function () {
    return {
      todoList: [] // 0:未完成 , 1:已完成 , 2:新增/修改
    }
  },
  methods:{
    addTodoList(){
      this.todoList.unshift({
        status: 2,
        text: '請輸入代辦事項'
      })  
    },
    editTodoList(n){
      this.todoList[n].status= 2;
    },
    removeTodoList(n){
      this.todoList.splice(n,1);
    },
    saveTodoList(n){
      this.todoList[n].status= 0;
    },
    completeTodoList(n,item){
      let completeItem = item;
      completeItem.status = 1
      this.todoList.splice(n,1);
      this.todoList.push(completeItem);
    },
    delCompleteTodoList(){
      for(var i = this.todoList.length -1; i >= 0 ; i--){
        if(this.todoList[i].status == 1){
            this.todoList.splice(i, 1);
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todoList {
  padding: 0 15px;
}
.todoList li {
  margin: 10px 0;
  padding-bottom: 2px;
  border-bottom: dashed 1px #ccc;
  width: 95%;
}
.todoList .complete {
  color: #999
}

.checkbox {
  border: solid 1px #16716c;
  background-color: #e8f3f2;
  position: relative;
  display: inline-block;
  width: 15px;
  height: 15px;
  border-radius: 3px;
  margin: 5px;
  vertical-align: middle;
}
.checkbox.disabled,.checkbox.checked {
  border: solid 1px #ccc;
  background-color: #eeeeee;
}
.checkbox.checked:before {
  content: '✔';
  position: absolute;
  top: -.3em;
  left: .1em;
  color: #ccc
}
.slide img {
  width: 100%;
}

.list-complete-item {
  transition: all .5s;
  display: inline-block;
  margin-right: 10px;
}
.list-complete-enter, .list-complete-leave-to
/* .list-complete-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateX(30px);
}
.list-complete-leave-active {
  position: absolute;
}
</style>
