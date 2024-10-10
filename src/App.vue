<template>
  <div id="app">
    <h1>待办事项列表</h1>
    <el-input v-model="newTodo" @keyup.enter="addTodo" placeholder="添加新的待办事项" />
    <el-button type="primary" @click="addTodo">添加</el-button>
    <el-table :data="todos" style="width: 100%">
      <el-table-column label="待办事项">
        <template #default="scope">
          <TodoItem :todo="scope.row" :index="scope.$index" @remove="removeTodo" @save="saveTodos" />
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem.vue';

export default {
  components: {
    TodoItem
  },
  data() {
    return {
      newTodo: '',
      todos: JSON.parse(localStorage.getItem('todos')) || []
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo.trim(), completed: false });
        this.newTodo = '';
        this.saveTodos();
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.saveTodos();
    },
    saveTodos() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
