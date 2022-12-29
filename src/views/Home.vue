<template>
  <div>
    <section>
      <input type="text" v-model="todo"  @keyup.enter="addTodo" placeholder="请输入待办事项:" />
      <a @click="clearData">clear</a>
      <ol class="demo-box">
        <template v-for="(item, index) in todoList">
          <li :key="index" v-if="item.done === false">
            <input type="checkbox" @change="changeTodo(index,true)">
            <p>{{item.todo}}</p>
            <a @click="deleteTodo(index,true)">✖</a>
          </li>
        </template>
      </ol>
      <ul>
        <template v-for="(item, index) in todoList">
          <li :key="index" v-if="item.done === true">
            <input type="checkbox" @change="changeTodo(index,false)" checked='checked'>
            <p>{{item.todo}}</p>
            <a @click="deleteTodo(index,false)">✖</a>
          </li>
        </template>
      </ul>
    </section>
  </div>
</template>

<script>
import * as Utils from '@/utils/utils'
export default {
  name: 'Todolist',
  data () {
    return {
      todo: '',
      todoList: [],
    }
  },
  methods: {
    initTodo () {
      var todoArr = Utils.getItem('todoList')
      if (todoArr) {
        this.todoList = todoArr
      }
    },
    addTodo () {
      let todoObj = {
        todo: this.todo,
        done: false
      }
      var tempList = Utils.getItem('todoList')
      if (tempList) {
        tempList.push(todoObj)
        Utils.setItem('todoList', tempList)
      } else {
        var tempData = []
        tempData.push(todoObj)
        Utils.setItem('todoList', tempData)
      }
      this.todoList.push(todoObj)
      this.todo = ''
    },
    deleteTodo (index) {
      this.todoList.splice(index, 1)
      Utils.setItem('todoList', this.todoList)
      
    },
    changeTodo (index, done) {
      if (done) {
        this.todoList[index].done = true
        Utils.setItem('todoList', this.todoList)
      } else {
        this.todoList[index].done = false
        Utils.setItem('todoList', this.todoList)
      }
    },
    clearData () {
      localStorage.clear()
      this.todoList = []
    }
  },
  mounted () {
    this.initTodo()
  }
}
</script>

<style scoped>
</style>
