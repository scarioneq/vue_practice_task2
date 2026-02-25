<template>
  <div class="app">
    <h1>Хранение заметок</h1>
    <div class="form-flex">
      <form
          @submit.prevent
      >
        <button
            @click="addCard()"
            class="btn btn-main"
        >
          Добавить карточку (в первый столбец)
        </button>
        <br>
        <br>
        <input
            class="input-create"
            type="text"
            placeholder="Название карточки"
            v-model="card.title"
        >
        <br>
        <input
            class="input-create"
            type="text"
            placeholder="Текст первой задачи"
            v-model="card.taskText.text1"
        >
        <br>
        <input
            class="input-create"
            type="text"
            placeholder="Текст второй задачи"
            v-model="card.taskText.text2"
        >
        <br>
        <input
            class="input-create"
            type="text"
            placeholder="Текст третьей задачи"
            v-model="card.taskText.text3"
        >
        <br>
        <button
            @click="showInput = true"
            v-if="!showInput"
            class="btn"
        >
          Добавить добавить еще пункт списка
        </button>

        <div
            v-if="showInput"
            class="add-task-input"
        >
          <input
              type="text"
              placeholder="Текст четвертой задачи"
              v-model="card.taskText.text4"
          >
          <button
              @click="showInput = false"
              class="btn"
          >
            Отмена
          </button>
        </div>
        <button
            v-if="card.taskText.text4 && !showFifthInput && showInput"
            @click="showFifthInput = true"
            class="btn"
        >
          Добавить добавить еще пункт списка
        </button>
        <div
            v-if="showFifthInput"
            class="add-task-input"
        >
          <input
              type="text"
              placeholder="Текст пятой задачи"
              v-model="card.taskText.text5"
          >
          <button
              @click="showFifthInput = false"
              class="btn"
          >
            Отмена</button>
        </div>
      </form>

    </div>
    <Board
        :cards="cards"
        @task-toggled="updateCompletedCards"
        @createTaskEvent="createTask"
        :block-second-column="blockSecondColumn"
    />
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
        taskText: {
          text1: '',
          text2: '',
          text3: '',
          text4: '',
          text5: '',
        }
      },
      showInput: false,
      showFifthInput: false,
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
      if (task.id === 6) {
        alert("Вы не можете создать больше пяти задач")
      } else {
        this.cards[card.id-1].tasks.push(task)
        this.saveToLocalStorage()
      }
    },
    addCard() {
      const cardsColumnOne = this.cards.filter(c => c.column === 1).length
      const filledCount = Object.values(this.card.taskText).filter(value => value !== '').length
      const taskArray = Object.values(this.card.taskText)
      let tasks = []
      if (this.card.title !=='' && filledCount >= 3) {
        if (!(cardsColumnOne >= 3)) {
          for (let i = 0; i < filledCount; i++) {
            const task = {
              id: i+1,
              text: taskArray[i],
              completed: false,
            }
            tasks.push(task)
          }
          const card = {
            id: this.cards.length + 1,
            title: this.card.title,
            column: 1,
            tasks: tasks
          }
          this.cards.push(card)
          this.card.title = ''
          this.card.taskText.text1 = ''
          this.card.taskText.text2 = ''
          this.card.taskText.text3 = ''
          this.card.taskText.text4 = ''
          this.card.taskText.text5 = ''
        }
        this.saveToLocalStorage()
      } else {
        alert("У карточки должно быть название и минимум 3 пункта списка")
      }
    },
    updateCompletedCards(data) {
      const card = this.cards.find(card => card.id === data.cardId)
      const task = card.tasks.find(task => task.id === data.taskId)
      task.completed = !task.completed
      this.editCardColumn(card, task)
      this.saveToLocalStorage()
    },
    editCardColumn(card, task) {
      const percent = this.getCardPercent(card)

      if (percent === 100) {
        card.column = 3
        card.completedAt = new Date().toLocaleString('sv-SE').replace(' ', ' ');
      } else if (percent >= 50 && this.cards.filter(c => c.column === 2).length !==5) {
        card.column = 2
        card.completedAt = ''
      } else {
        if (!this.cards.filter(c => c.column === 1).length >= 3) {
          console.log('123')
          card.column = 1
          card.completedAt = ''
        } else {
          alert("Вы не можете убрать завершения пункта задачи, так как в первом столбце уже максимальное число карточек")
          task.completed = !task.completed
        }
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
        const percent = this.getCardPercent(card)
        if (percent >= 50 && this.cards.filter(c => c.column === 2).length < 5) {
          card.column = 2
        }
      })
      this.saveToLocalStorage()
    },
    getCardPercent(card) {
      const total = card.tasks.length
      const completed = card.tasks.filter(t => t.completed).length
      return total === 0 ? 0 : (completed / total) * 100
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

.btn {
  padding: 5px;
  border-radius: 6px;
  border: 1px solid teal;
  background-color: white;
}

.form-flex {
  display: inline;
}

.input-create {
  width: 30%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid teal;
}

.btn-main {
  padding: 15px;
  border: 2px solid teal;
}




</style>