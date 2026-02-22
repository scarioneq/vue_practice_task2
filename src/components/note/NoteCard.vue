<template>
  <div class="note-card">
    <h3>{{ card.title }}</h3>

    <div class="todo">
      <ol>
        <li v-for="task in card.tasks" :key="task.id">
          <label>
            <input
                type="checkbox"
                :checked="task.completed"
                @change="toggleTask(task.id)"
            >
            {{ task.text }}
          </label>
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
  methods: {
    toggleTask(taskId) {
      this.$emit('task-toggled', {
        cardId: this.card.id,
        taskId: taskId
      })
    }
  }
}
</script>

<style>

</style>