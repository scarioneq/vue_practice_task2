<template>
  <div class="board">
    <Column
        title="Новые задачи"
        :cards="cards.filter(card => card.column === 1)"
        :limit="3"
        @task-toggled="$emit('task-toggled', $event)"

    />
    <Column
        title="Почти закончили"
        :cards="cards.filter(card => card.column === 2)"
        :limit="5"
        @task-toggled="$emit('task-toggled', $event)"
    />
    <Column
        title="Завершено"
        :cards="cards.filter(card => card.column === 3)"
        @task-toggled="$emit('task-toggled', $event)"
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
    }
  }
}
</script>

<style >

</style>