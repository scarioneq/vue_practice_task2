<template>
  <div class="app">
    <h1>Хранение заметок</h1>
    <div class="btn-card">
      <form @submit.prevent>
        <button @click="addCard()">Добавить карточку (в первый столбец)</button>
        <br>
        <input
            type="text"
            placeholder="Название карточки"
            v-model="card.title"
        >
      </form>

    </div>
    <Board :cards="cards" @task-toggled="updateCompletedCards" @createTaskEvent="createTask"/>
  </div>
</template>

<script>

import Board from "@/components/board/Board.vue";

export default {
  components: {Board},
  data() {
    return {
      card : {
        title: '',
      },
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
  },
  methods: {
    createTask() {
      console.log('1234');
    },
    addCard() {
      // console.log(this.cards.length + "", this.card.title)
      const cardsColumnOne = this.cards.filter(c => c.column === 1).length
      // console.log(cardsColumnOne)

      if (!(cardsColumnOne >= 3)) {
        const card = {
          id: this.cards.length + 1,
          title: this.card.title,
          column: 1,
          tasks: []
        }
        this.cards.push(card)
      }
    },
    updateCompletedCards(data) {
      const card = this.cards.find(card => card.id === data.cardId)

      const task = card.tasks.find(task => task.id === data.taskId)
      task.completed = !task.completed
      this.editCardColumn(card, task)
    },
    editCardColumn(card, task) {
      const total = card.tasks.length
      const completed = card.tasks.filter(t => t.completed).length
      const percent = total === 0 ? 0 : (completed / total) * 100
      if (percent >=100) {
        card.column = 3
      } else if (percent >= 50) {
        card.column = 2
      } else {
        card.column = 1
      }
    },

  },
  computed: {

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