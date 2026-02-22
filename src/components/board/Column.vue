<template>
    <div class="column">
      <h2> {{ title }}</h2>
      <div v-if="limit" class="column-info">
        Карточек: {{ cards.length }} // {{ limit }}
      </div>
      <NoteCard
          v-for="card in cards"
          :key="card.id"
          :card="card"
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
      default: () => []
    },
    limit: {
      type: Number,
      default: null
    }
  }

}
</script>

<style>

</style>