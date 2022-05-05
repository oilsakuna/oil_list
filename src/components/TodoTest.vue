<template>
  <div class="container shadow-lg px-5 py-5 rounded-3">
    <h1 class="mb-5">oil 🐮 list</h1>
    <i class="fa-solid fa-user"></i>
    <div class="h2 mb-0">
      <b-icon-arrow-up></b-icon-arrow-up>

      <b-icon-exclamation-triangle-fill></b-icon-exclamation-triangle-fill>
    </div>

    <div class="d-flex mb-5">
      <input
        v-model="newTodo"
        type="text"
        placeholder="Enter To Do"
        class="form-control form-input me-3"
      />
      <button type="submit" class="submit-btn px-3 py-2" @click="addTodo()">
        +
      </button>
    </div>

    <!-- <div
      class="row todo-list shadow px-3 pt-3 pb-2 align-items-center mb-4"
      v-for="(todo, index) in todos"
      :key="index"
    >
    <div class="col-10 text-start" @click="Todo()">
      <input type="checkbox" v-model="todo.done" />

      <p :style="todo.done && { textDecoration: 'line-through' }">
        {{ todo.name }}
      </p>
</div>
        <h5 :class="{ 'todo-finished': todo.status === 'finished' }">
          {{ todo.name }}
        </h5>
         -->
    <div
      class="row todo-list shadow px-3 pt-3 pb-2 align-items-center mb-4"
      v-for="(todo, index) in todos"
      :key="index"
    >
      <div class="col-10 text-start" @click="editTodo(index)">
        <input type="checkbox" v-model="todo.done" />
        <div>
          <p :style="todo.done && { textDecoration: 'line-through' }">
            {{ todo.name }}
          </p>
        </div>
      </div>

      <div class="col-2">
        <div class="d-flex justify-content-start align-items-right">
          <button
            type="submit"
            class="delete-btn px-3 py-2"
            @click="removeTodo(todo)"
          >
            X
          </button>
          <button
            type="submit"
            class="edit-btn px-3 py-2"
            @click="editTodo(index)"
          >
            Edit
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      newTodo: "",
      indexEditTodo: null,
      tempNameTodo: "",
      tempStatusTodo: "",
      todoStatus: ["to-do", "on-going", "finished"],
      todos: [
        {
          name: "Kompan",
          status: "to-do",
        },
        {
          name: "kittitara",
          status: "finished",
        },
        {
          name: "sakuna",
          status: "on-going",
        },
      ],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length === 0) return;
      if (this.indexEditTodo === null) {
        this.todos.push({
          name: this.newTodo,
          status: "to-do",
        });
      } else {
        this.todos[this.indexEditTodo].name = this.newTodo;
        this.indexEditTodo = null;
      }
      this.newTodo = "";
    },
    removeTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
    },
    editTodo(index) {
      this.newTodo = this.todos[index].name;
      this.indexEditTodo = index;
    },
  },
};
</script>

<style scoped>
.form-input {
  border: 1px solid #333;
  border-radius: 50px;
}
.form-control:focus {
  box-shadow: none;
}
.submit-btn {
  background-color: rgb(74, 231, 12);
  border-radius: 50%;
  border: none;
  font-size: 20px;
  font-weight: 800;
  color: #fff;
}
.delete-btn {
  background-color: rgb(255, 15, 55);
  border-radius: 50%;
  border: none;
  font-size: 20px;
  font-weight: 800;
  color: #fff;
}
.edit-btn {
  background-color: rgb(195, 248, 4);
  border-radius: 50%;
  border: none;
  font-size: 20px;
  font-weight: 800;
  color: #fff;
}
.todo-list {
  border-radius: 50px;
}
</style>
