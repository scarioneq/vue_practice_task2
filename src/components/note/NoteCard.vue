<template>
  <div class="note-card">
    <h3>{{ card.title }}</h3>

    <div class="todo">
      <ol>
        <li v-for="task in card.tasks" :key="task.id">
            <input
                type="checkbox"
                :checked="task.completed"
                @change="toggleTask(task)"

            >
            {{ task.text }}
        </li>
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
  },
  emits: ['task-toggled'],

  methods: {
    toggleTask(task) {
      this.$emit('task-toggled', {
        cardId: this.card.id,
        taskId: task.id,
        completed: task.completed
      })
    },

  }
}
</script>

<style>

</style>