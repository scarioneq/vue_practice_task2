<template>
  <div class="board">
    <Column
        title="Столбец 1"
        :cards="cards.filter(card => card.column === 1)"
        :limit="3"
    />
    <Column
        title="Столбец 2"
        :cards="cards.filter(card => card.column === 2)"
        :limit="5"
    />
    <Column
        title="Столбец 3"
        :cards="cards.filter(card => card.column === 1)"
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