<template>
  <div class="student">
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <h2>学生年龄：{{ age }}</h2>
    <button @click="sendStudentName">事件总线</button>
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
    sendStudentName() {
      this.$bus.$emit("hello",this.name);
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
