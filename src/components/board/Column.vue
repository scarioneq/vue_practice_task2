<template>
  <div>
    <div class="column">
      <h2>Колонка</h2>
      <NoteCard />
      <NoteCard />
    </div>

  </div>
</template>

<script>
import NoteCard from "@/components/note/NoteCard.vue";

export default {
  components: {NoteCard}

}
</script>

<style>

</style>