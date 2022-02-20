<template>
  <div class="student">
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <h2>学生年龄：{{ age }}</h2>
    <button @click="sendStudentName">发布消息</button>
  </div>
</template>

<script>
import pubsub from 'pubsub-js'

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
    sendStudentName() {
      // this.$bus.$emit('hello',this.name)
      pubsub.publish('hello', 666)
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
