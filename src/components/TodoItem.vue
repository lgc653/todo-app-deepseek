<template>
  <el-checkbox v-model="todo.completed" @change="saveTodos">
    <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
  </el-checkbox>
  <el-button type="danger" @click="removeTodo">移除</el-button>
</template>

<script>
export default {
  props: {
    todo: Object,
    index: Number
  },
  methods: {
    removeTodo() {
      this.$emit('remove', this.index);
    },
    saveTodos() {
      this.$emit('save');
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
