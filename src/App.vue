<template>
  <div class="app">
    <h1>Хранение заметок</h1>
    <div class ="btn-card">
      <button>Добавить карточку (в первый столбец)</button>
    </div>
    <div class="board">
      <div class="column">
        <h2>Столбец 1</h2>
        <div class="note-card">
          <h3>Карточка 1</h3>
          <div class="todo">
            <ol>
              <li>Задача 1</li>
              <li>Задача 2</li>
              <li>Задача 3</li>
            </ol>
          </div>
          <div class="btn-add-do">
            <input type="text">
            <button>Добавить задачу</button>
          </div>

        </div>
        <div class="note-card">
          <h3>Карточка 2</h3>
          <div class="todo">
            <ol>
              <li>Задача 1</li>
              <li>Задача 2</li>
              <li>Задача 3</li>
            </ol>
          </div>
          <div class="btn-add-do">
            <input type="text">
            <button>Добавить задачу</button>
          </div>
        </div>
      </div>
      <div class="column">
        <h2>Столбец 2</h2>
        <div class="note-card">
          <h3>Карточка 1</h3>
          <div class="todo">
            <ol>
              <li>Задача 1</li>
              <li>Задача 2</li>
              <li>Задача 3</li>
            </ol>
          </div>
          <div class="btn-add-do">
            <input type="text">
            <button>Добавить задачу</button>
          </div>
        </div>
      </div>
      <div class="column">
        <h2>Столбец 3</h2>
        <div class="note-card">
          <h3>Карточка 1</h3>
          <div class="todo">
            <ol>
              <li>Задача 1</li>
              <li>Задача 2</li>
              <li>Задача 3</li>
            </ol>
          </div>
          <div class="btn-add-do">
            <input type="text">
            <button>Добавить задачу</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {

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