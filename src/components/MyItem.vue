<template>
  <li>
    <label>
      <input type="checkbox"
             :checked="todo.done"
             @change="handleCheck(todo.id)"/>
      <!-- 如下代码也能实现功能，但是不太推荐，因为有点违反原则，因为修改了props -->
      <!-- <input type="checkbox" v-model="todo.done"/> -->
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input type="text"
             v-show="todo.isEdit"
             :value="todo.title"
             @blur="handleBlur(todo,$event)"/>
    </label>
    <button class="btn btn-danger"
            @click="handleDelete(todo.id)">删除
    </button>
    <button class="btn btn-info"
            v-show="!todo.isEdit"
            @click="handleEdit(todo)">编辑
    </button>
  </li>
</template>

<script>

import pubsub from "pubsub-js";

export default {
  name: "MyItem",
  props: ['todo'],
  methods: {
    handleCheck(id) {
      this.$bus.$emit('checkTodo', id)
    },
    handleDelete(id) {
      if (confirm("确认要删除任务吗？")) {
        // this.$bus.$emit('deleteTodo', id)
        pubsub.publish('deleteTodo', id)
      }
    },
    handleEdit(todo) {
      // eslint-disable-next-line no-prototype-builtins
      if (!todo.hasOwnProperty('isEdit')) {
        this.$set(todo, 'isEdit', true);
      } else {
        todo.isEdit = true;
      }
    },

    handleBlur(todo, event) {
      todo.isEdit = false;
      if (!event.target.value.trim()) {
        return alert("任务不能为空")
      } else {
        this.$bus.$emit('editTodo', todo.id, event.target.value)
      }
    }
  },

}
</script>


<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>