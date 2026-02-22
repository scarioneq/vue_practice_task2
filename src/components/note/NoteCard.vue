<template>
  <div class="note-card">
    <h3>{{ card.title }}</h3>

    <div>Задач: {{ card.tasks.length || 0 }}</div>

    <div class="todo">
      <ol>
        <li v-if="card.tasks.length" v-for="task in card.tasks" :key="task.id">
          {{ task.text }} - {{ task.completed ? 'true' : 'false' }}
        </li>
        <li v-else>Нет задач</li>
      </ol>
    </div>

    <div class="btn-add-do">
      <input type="text">
      <button>Добавить задачу</button>
    </div>
  </div>
</template>

<script>


export default {
  props: {
    card: {
      type: Object,
      required: true
    }
  }

}
</script>

<style>

</style>