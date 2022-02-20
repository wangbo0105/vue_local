<template>
  <div class="app">
    <h1>{{ msg }}:{{name}}</h1>
    <!-- 通过父组件给子组件传递函数类型的props实现：子给父传递数据 -->
    <school :getSchoolName="getSchoolName"/>

    <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第一种写法，使用@或v-on） -->
    <!--    <student @sendName="getStudentName"/>-->
    <!--    一次性-->
    <!--    <student @sendName.once="getStudentName"/>-->


    <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第二种写法，使用ref） -->
    <student ref="student"/>


  </div>
</template>

<script>
import Student from './components/Student'
import School from './components/School'

export default {
  name: 'App',
  data() {
    return {
      msg: "你好啊",
      name: "",
    }
  },
  components: {School, Student},
  methods: {
    getSchoolName(name) {
      console.log("学校名称：", name);
    },
    getStudentName(name) {
      this.name = name;
      console.log("学生姓名：", name);

    }
  },
  mounted() {
    //绑定自定义事件
    this.$refs.student.$on("sendName", this.getStudentName);

    //绑定自定义事件（一次性）
    // this.$refs.student.$once('sendName', this.getStudentName)

    // setTimeout(() => {
    //   this.$destroy()
    // }, 3000)
  }
}
</script>

<style>
.app {
  background-color: gray;
  padding: 10px;
}
</style>
