<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!--      <input type="checkbox" :checked="checked" @change="handleCheck"/>-->
      <input type="checkbox" v-model="checked"/>

    </label>
    <span>
			<span>已完成{{ doneTotal }}</span> / 全部{{ total }}
		</span>
    <button class="btn btn-danger" @click="handleClear">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ['todos'],
  methods: {
    handleCheck(event) {
      this.$emit("checkAllTodo",event.target.checked)
    },
    handleClear(){
      this.$emit("clearAllDoneTodo")
    }
  },
  computed: {
    total() {
      return this.todos.length;
    },
    doneTotal() {
      return this.todos.reduce((previousValue, currentValue) => previousValue + (currentValue.done ? 1 : 0), 0)
    },
    // checked() {
    //   return this.total === this.doneTotal && this.total > 0;
    // }
    checked: {
      get() {
        return this.total === this.doneTotal && this.total > 0;
      },
      set(value) {
        this.$emit("checkAllTodo",value);
      }
    }
  },
}
</script>
<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>