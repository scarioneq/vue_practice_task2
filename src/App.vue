<template>
  <div class="app">
    <h1>Хранение заметок</h1>
    <div class="btn-card">
      <button>Добавить карточку (в первый столбец)</button>
    </div>
    <Board :cards="cards" />
  </div>
</template>

<script>

import Board from "@/components/board/Board.vue";

export default {
  components: {Board},
  data() {
    return {
      cards: [
        {
          id: 1,
          title: 'Учеба',
          column: 1,
          tasks: [
            {id: 1, text: 'Выучить Vue', completed: false},
            {id: 2, text: '10 лаб по КС', completed: false},
          ],
        },
        {
          id: 2,
          title: 'Покупки',
          column: 1,
          tasks: [
            {id: 1, text: 'Quest 2', completed: false},
          ],
        },
        {
          id: 3,
          title: 'php',
          column: 1,
          tasks: [
            {id: 1, text: 'Разобраться с ОПП', completed: true},
          ],
        },
        {
          id: 4,
          title: 'JavaScript',
          column: 2,
          tasks: [
            {id: 1, text: 'Синтаксис', completed: true},
            {id: 2, text: 'Разобраться с ОПП', completed: true},
            {id: 3, text: 'Async', completed: false},
          ],
        },
      ],
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