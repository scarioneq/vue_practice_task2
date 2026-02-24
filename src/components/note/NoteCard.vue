<template>
  <div
      class="note-card"
  >
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
      <div>
        {{card.completedAt}}
      </div>
    </div>

    <form @submit.prevent class="btn-add-do" >
      <input
          type="text"
          placeholder="Текст задачи"
          v-model="task.text"
      >
      <button
          @click="createTask"
      >Добавить задачу</button>
    </form>
  </div>
</template>

<script>

export default {
  data() {
    return {
      task: {
        text: ''
      }
    }
  },
  props: {
    card: {
      type: Object,
      required: true
    }
  },
  emits: ['task-toggled', 'createTaskEvent'],

  methods: {
    createTask() {
      this.$emit('createTaskEvent', {
        card: this.card,
        taskText: this.task.text,
      })
      this.task.text = ''
    },

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