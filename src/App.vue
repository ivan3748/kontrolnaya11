<template>
  <div id="app">
    <header>
      <h1>Список задач</h1>
    </header>
    <main>
      <div class="todo-app">
        <form @submit.prevent="addTask">
          <input
            v-model="newTask"
            placeholder="Введите задачу"
            class="task-input"
          />
          <button type="submit" class="add-btn">Добавить</button>
        </form>
        <ul class="task-list">
          <li v-for="(task, index) in tasks" :key="index" :class="{ done: task.done }">
            <label>
              <input type="checkbox" v-model="task.done" />
              {{ task.title }}
            </label>
            <button @click="removeTask(index)" class="remove-btn">Удалить</button>
          </li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ title: this.newTask.trim(), done: false });
        this.newTask = "";
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style scoped>
/* Обновлённая цветовая гамма */
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background: linear-gradient(to bottom, #eef2f3, #8e9eab);
  min-height: 100vh;
}

#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

header h1 {
  text-align: center;
  font-size: 2.5em;
  font-weight: bold;
  color: transparent;
  background: linear-gradient(to right, #ff7e5f, #feb47b);
  -webkit-background-clip: text;
  background-clip: text;
  margin-bottom: 20px;
}

.todo-app {
  background: white;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}

.task-input {
  width: calc(100% - 100px);
  padding: 10px;
  border: 2px solid #ff7e5f;
  border-radius: 8px;
  font-size: 1em;
}

.add-btn {
  padding: 10px 20px;
  background: linear-gradient(to right, #ff7e5f, #feb47b);
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1em;
}

.add-btn:hover {
  background: linear-gradient(to right, #feb47b, #ff7e5f);
}

.task-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

.task-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.task-list li.done {
  text-decoration: line-through;
  color: gray;
}

.remove-btn {
  background: none;
  border: none;
  color: #ff7e5f;
  cursor: pointer;
}

.remove-btn:hover {
  color: #e6492d;
}
</style>
