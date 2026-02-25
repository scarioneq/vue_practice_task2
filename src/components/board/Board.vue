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

.board {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  flex-direction: row;
  gap: 100px;
  justify-content: space-between;
  background-color: #ebefeb;
}


</style>