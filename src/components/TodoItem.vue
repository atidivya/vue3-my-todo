<template>
  <div class="todo-item" @click="importantTodo(todo.id)">
    <div class="user-profile_todo">
      <div class="todo-item_user">
        {{username}}
      </div>
      <div class="todo-item_content">
        {{todo.content}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props:{
        username:{
            type: String,
            required: true
        },
        todo:{
            type: Object,
            required: true
        }
    },
    methods: {
        importantTodo(id) {
            this.$emit('important', id)
        }
    }
};
</script>

<style lang="scss" scoped>
.todo-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;

  &:hover {
  transform: scale(1.1, 1.1);
}

  .todo-item_user { 
  font-weight: bold;
}
}




</style>
