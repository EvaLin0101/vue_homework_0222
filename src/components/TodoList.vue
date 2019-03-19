<template>
  <div class="todoList">
    <div class="functionBtn">
      <button @click="addTodoList" class="green">新增</button>
      <button @click="delCompleteTodoList">刪除完成項目</button>
    </div>
    <p v-if="todoList.length == 0">目前沒有任何待辦事項</p>
    <transition-group name="list-complete" tag="ul">
      <li v-for="(item,index) in todoList" :key="index" class="list-complete-item">
        <TodoItem :index="index" :item="item" @complete="completeTodoList"/>
        <button v-if="item.status == 'todo'" @click="editTodoList(index)">修改</button>
        <button v-if="item.status == 'todo'" @click="removeTodoList(index)">刪除</button>
        <button v-if="item.status == 'edit'" @click="saveTodoList(index)" class="green">儲存</button>
      </li>
    </transition-group>
  </div>
</template>

<script>
import TodoItem from "../components/TodoItem.vue";
export default {
  name: "TodoList",
  components: {
    TodoItem
  },
  data: function() {
    return {
      todoList: [],
      editing: false
    };
  },
  methods: {
    addTodoList() {
      if (this.editing) {
        alert("edit");
      } else {
        this.todoList.unshift({
          status: "edit",
          text: "請輸入代辦事項"
        });
        this.editing = true;
      }
    },
    editTodoList(n) {
      if (this.editing) {
        alert("edit");
      } else {
        this.todoList[n].status = "edit";
        this.editing = true;
      }
    },
    completeTodoList(n) {
      let completeItem = this.todoList[n];
      completeItem.status = "complete";
      this.todoList.splice(n, 1);
      this.todoList.push(completeItem);
    },
    removeTodoList(n) {
      this.todoList.splice(n, 1);
    },
    saveTodoList(n) {
      this.todoList[n].status = "todo";
      this.editing = false;
    },
    delCompleteTodoList() {
      for (var i = this.todoList.length - 1; i >= 0; i--) {
        if (this.todoList[i].status == "complete") {
          this.todoList.splice(i, 1);
        }
      }
    }
  }
};
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
.list-complete-item {
  transition: all 0.5s;
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
