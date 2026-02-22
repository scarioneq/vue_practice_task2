<template>
  <div class="app">
    <h1>Хранение заметок</h1>
    <div class="btn-card">
      <button>Добавить карточку (в первый столбец)</button>
    </div>
    <Board />
  </div>
</template>

<script>

import Board from "@/components/board/Board.vue";

export default {
  components: {Board},
  data() {
    return {
      cards: [
        {id: 1, title: 'Карточка 1', column: 1, tasks: ['123', '321']},
        {id: 2, title: 'Карточка 1', column: 1, tasks: ['123', '321']},
        {id: 3, title: 'Карточка 1', column: 1, tasks: ['123', '321']},
      ]
    }
  }

}
</script>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.board {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  flex-direction: row;
  gap: 100px;
  justify-content: space-between;
  background-color: #c2e4c6;
}

.column {
  border: 1px solid teal;
  background-color: #ecf4ec;
}

.note-card {
  border: 1px solid teal;
}

.todo {
  border: 1px solid teal;
}

</style>