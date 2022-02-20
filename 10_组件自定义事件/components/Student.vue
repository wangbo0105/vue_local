<template>
  <div class="student">
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <h2>学生年龄：{{ age }}</h2>
    <button @click="addAge">改变年龄</button>
    <button @click="sendStudentName">绑定自定义事件</button>
    <button @click="unbind">解绑自定义事件</button>
    <button @click="kill">销毁student组件</button>


  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Student',
  data() {
    return {
      name: '小码',
      sex: '男',
      age: 18
    }
  },
  methods: {
    addAge() {
      this.age++;
      console.log("当前年龄：", this.age);

    },
    sendStudentName() {
      this.$emit("sendName", this.name);
    },
    unbind() {
      //解绑一个自定义事件
      this.$off('sendName')

      //解绑多个自定义事件
      // this.$off(['sendName','xxx'])

      //解绑所有的自定义事件
      // this.$off()
    },
    // 销毁了当前Student组件的实例，销毁后所有Student实例的自定义事件全都不奏效。
    kill() {
      this.$destroy();
    }
  },
}
</script>

<style scoped>
.student {
  background-color: pink;
  padding: 5px;
  margin-top: 20px;
}

button {
  margin: 0 5px;
}
</style>
