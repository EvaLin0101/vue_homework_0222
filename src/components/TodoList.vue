<template>
  <div class="todoList">
    <div class="functionBtn">
      <button @click="addTodoList" class="green">新增</button>
      <button @click="delCompleteTodoList">刪除完成項目</button>
    </div>
    <ul>
      <li v-if="todoList.length==0">目前沒有任何待辦事項</li>
      <li v-for="(item,index) in todoList" :key="index">
        <span v-if="item.status == 0">
          <input type="checkbox" @click="completeTodoList(index,item)"/>{{item.text}}
        </span>
        <span v-if="item.status == 1" class="complete">
          <input type="checkbox" checked disabled />{{item.text}}
        </span>
        <span v-if="item.status == 2">
          <input type="checkbox" disabled/><input type="text" v-model="item.text"/>
        </span>
        <button v-if="item.status == 0" @click="editTodoList(index)">修改</button>
        <button v-if="item.status == 0" @click="removeTodoList(index)">刪除</button>
        <button v-if="item.status == 2" @click="saveTodoList(index)" class="green">儲存</button>
      </li>
    </ul>
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
  mounted: function () {
    this.addTodoList('text')
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
.todoList li {
  margin: 10px 0;
}
.todoList .complete {
  color: #999
}
.slide img {
  width: 100%;
}

</style>
