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
    <Board :cards="cards" @task-toggled="updateCompletedCards" @createTaskEvent="createTask" :block-second-column="blockSecondColumn"/>
  </div>
</template>

<script>

import Board from "@/components/board/Board.vue";

export default {
  created() {
    this.loadFromLocalStorage()
  },

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
          completedAt: '123'
        },
        {
          id: 2,
          title: 'Покупки',
          column: 2,
          tasks: [
            {id: 1, text: 'Quest 2', completed: false, completedAt: ''},
          ],
          completedAt: ''
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
          completedAt: ''
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
          completedAt: ''
        },
        {
          id: 5,
          title: 'JavaScript',
          column: 2,
          tasks: [
            {id: 1, text: 'Синтаксис', completed: true},
            {id: 2, text: 'Разобраться с ОПП', completed: true},
            {id: 3, text: 'Async', completed: false},
          ],
          completedAt: ''
        },
      ],
      blockSecondColumn: false
    }
  },
  methods: {
    loadFromLocalStorage() {
      const savedCards = localStorage.getItem('cards')
      const savedBlockState = localStorage.getItem('blockSecondColumn')

      if (savedCards) {
        this.cards = JSON.parse(savedCards)
      }

      if (savedBlockState) {
        this.blockSecondColumn = JSON.parse(savedBlockState)
      }
    },
    saveToLocalStorage() {
      localStorage.setItem('cards', JSON.stringify(this.cards))
      localStorage.setItem('blockSecondColumn', JSON.stringify(this.blockSecondColumn))
    },
    createTask(data) {
      const taskText = data.taskText
      const card = data.card
      const task = {
        id: card.tasks.length + 1,
        text: taskText,
        completed: false,
      }
      this.cards[card.id-1].tasks.push(task)
      this.saveToLocalStorage()
    },
    addCard() {
      const cardsColumnOne = this.cards.filter(c => c.column === 1).length

      if (!(cardsColumnOne >= 3)) {
        const card = {
          id: this.cards.length + 1,
          title: this.card.title,
          column: 1,
          tasks: []
        }
        this.cards.push(card)
        this.card.title = ''
      }
      this.saveToLocalStorage()
    },
    updateCompletedCards(data) {
      const card = this.cards.find(card => card.id === data.cardId)
      const task = card.tasks.find(task => task.id === data.taskId)
      task.completed = !task.completed
      this.editCardColumn(card, task)
      this.saveToLocalStorage()
    },
    editCardColumn(card) {
      const total = card.tasks.length
      const completed = card.tasks.filter(t => t.completed).length
      const percent = total === 0 ? 0 : (completed / total) * 100

      if (percent >=100) {
        card.column = 3
        card.completedAt = new Date().toLocaleString('sv-SE').replace(' ', ' ');
      } else if (percent >= 50 && this.cards.filter(c => c.column === 2).length !==5) {
        card.column = 2
        card.completedAt = ''
      } else {
        card.column = 1
        card.completedAt = ''
      }

      if (percent >= 50 && this.cards.filter(c => c.column === 2).length === 5 && card.column === 1) {
        this.blockSecondColumn = true
      }
      if (percent >=100 && card.column === 3 && this.cards.filter(c => c.column === 2).length !== 5 && this.blockSecondColumn) {
        this.blockSecondColumn = false
        this.updateFirstColumnCards()
      }
      if (percent < 50 && this.cards.filter(c => c.column === 2).length === 5 && card.column === 1) {
        this.blockSecondColumn = false
      }
      this.saveToLocalStorage()

    },
    updateFirstColumnCards() {
      const firstColumnCards = this.cards.filter(c => c.column === 1)

      firstColumnCards.forEach(card => {
        const total = card.tasks.length
        const completed = card.tasks.filter(t => t.completed).length
        const percent = total === 0 ? 0 : (completed / total) * 100
        if (percent >= 50 && this.cards.filter(c => c.column === 2).length < 5) {
          card.column = 2
        }
      })
      this.saveToLocalStorage()
    }

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