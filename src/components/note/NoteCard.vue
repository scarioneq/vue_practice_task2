<template>
  <div class="note-card">
    <h3>Карточка 1</h3>
    <TodoList />
    <div class="btn-add-do">
      <input type="text">
      <button>Добавить задачу</button>
    </div>
  </div>
</template>

<script>
import TodoList from "@/components/note/TodoList.vue";

export default {
  components: {TodoList}

}
</script>

<style>

</style>