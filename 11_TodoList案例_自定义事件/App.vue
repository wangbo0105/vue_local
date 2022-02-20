<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <my-header @addTodo="addTodo"/>
        <my-list :todos="todos"
                 :checkTodo="checkTodo"
                 :deleteTodo="deleteTodo"/>
        <my-footer :todos="todos"
                   @checkAllTodo="checkAllTodo"
                   @clearAllDoneTodo="clearAllDoneTodo"/>

      </div>
    </div>
  </div>

</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyList from './components/MyList.vue'
import MyFooter from './components/MyFooter.vue'


export default {
  name: 'App',
  components: {
    MyHeader, MyList, MyFooter
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    // 添加一个tido
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    // 更新todo完成状态
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.done = !todo.done;
        }
      })
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id;
      })
    },
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      })
    },
    clearAllDoneTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done;
      })
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(newValue) {
        localStorage.setItem("todos", JSON.stringify(newValue));
      }
    }
  },
  mounted() {
    const todoStorage = JSON.parse(localStorage.getItem("todos"))
    this.todos = todoStorage || [];
  },
}
</script>


<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>

