<template>
  <div class="item-content" :class="itemStatus">
      <span @click="complete(index)" class="checkbox"></span> 
      <span v-if="itemStatus!='edit'">{{item.text}}</span>
      <input v-else type="text" v-model="item.text"/>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    index: Number,
    item: Object
  },
  computed: {
    itemStatus: function() {
      return this.item.status;
    }
  },
  methods: {
    complete(n) {
      if (this.itemStatus == "todo") {
        this.$emit("complete", n);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.item-content {
  display: inline-block;
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
.edit .checkbox,
.complete .checkbox {
  border: solid 1px #ccc;
  background-color: #eeeeee;
}
.complete .checkbox:before {
  content: "✔";
  position: absolute;
  top: -0.3em;
  left: 0.1em;
  color: #ccc;
}
.complete {
  color: #999;
}
</style>
