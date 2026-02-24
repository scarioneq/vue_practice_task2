<template>
  <div class="board">
    <Column
        title="Новые задачи"
        :cards="cards.filter(card => card.column === 1)"
        :limit="3"
        :block-second-column="blockSecondColumn"
        @task-toggled="$emit('task-toggled', $event)"
        @createTaskEvent="$emit('createTaskEvent', $event)"

    />
    <Column
        title="Почти закончили"
        :cards="cards.filter(card => card.column === 2)"
        :limit="5"
        :block-second-column="blockSecondColumn"
        @task-toggled="$emit('task-toggled', $event)"
        @createTaskEvent="$emit('createTaskEvent', $event)"
    />
    <Column
        title="Завершено"
        :cards="cards.filter(card => card.column === 3)"
        :block-second-column="blockSecondColumn"
        @task-toggled="$emit('task-toggled', $event)"
        @createTaskEvent="$emit('createTaskEvent', $event)"
    />
  </div>
</template>

<script>
import Column from "@/components/board/Column.vue";

export default {
  components: {Column},
  props: {
    cards: {
      type: Array,
      required: true
    },
    blockSecondColumn: {
      type: Boolean,
      required: true
    }
  },

}
</script>

<style >
.block-first-column {
  pointer-events: none;
  opacity: 0.5;
}


</style>