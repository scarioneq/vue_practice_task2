<template>
    <div class="column" :class="{ 'block-first-column': blockSecondColumn && title === 'Новые задачи' }">
      <h2> {{ title }}</h2>
      <div v-if="limit" class="column-info">
        Карточек: {{ cards.length }} // {{ limit }}
      </div>
      <NoteCard
          v-for="card in cards"
          :key="card.id"
          :card="card"
          @task-toggled="$emit('task-toggled', $event)"
          @createTaskEvent="$emit('createTaskEvent', $event)"
      />
    </div>

</template>

<script>
import NoteCard from "@/components/note/NoteCard.vue";

export default {
  components: {NoteCard},
  props: {
    title: {
      type: String,
      required: true
    },
    cards: {
      type: Array,
      required: true
    },
    limit: {
      type: Number,
      default: null
    },
    blockSecondColumn: {
      type: Boolean,
      required: true
    }
  },
  computed: {

  }
}
</script>

<style>



</style>