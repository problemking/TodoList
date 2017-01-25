<template>
  <div id="app">
    <h1 v-text="msg"></h1>
    <input type="text" v-model="newtodo" @keyup.enter="add">
    <ul>
      <li is="todo" v-for="(item,index) in todoList" :item="item" :index="index" @delete="deleteTodo"></li>
    </ul>
  </div>
</template>
<script>
  import Todo from './components/todo'
  export default {
  data () {
    return {
      msg:"This is a todo list",
      newtodo:'',
      todoList:[]
    }
  },
  components:{
      Todo
  },
  methods:{
    add(){
      this.todoList.push(this.newtodo)
      this.newtodo=""
    },
    deleteTodo (index) {
      // 删除指定项列表
      this.todoList.splice(index, 1)
    }
  },
  watch: {
    todoList (newList) {
      // 监听组件列表数据并将其保存到localstorage中
      console.log(newList)
      localStorage.setItem('vueTodoList', JSON.stringify(newList))
    }
  },
  mounted () {
    this.todoList=JSON.parse(localStorage.getItem('vueTodoList')|| '[]')
  },
}

</script>

<style scoped>
#app {
  text-align: center;
  color: red;
  margin-top: 60px;
}

input[type="text"]{
    width: 300px;
  }
</style>
