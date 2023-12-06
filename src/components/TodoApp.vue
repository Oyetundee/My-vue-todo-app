<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model='todo' type="text" placeholder="Enter todo" class="form-control">
      <button @click="submitTodo" class="btn btn-success rounded-0"><b>Enter</b></button>
    </div>

    <!-- Todo Table -->
    <table class="table table-hover mt-5">
      <thead>
        <tr>
          <th scope="col">Todo</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="index">
          <td>{{ todo.name }}</td>
          <td>Finished</td>
          <td>
            <div class="text-center" @click="editTodo(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTodo(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Display all todos when button is clicked -->
    <div class="mt-5">
      <h3>All Todos</h3>
      <button @click="showAllTodos" class="btn btn-primary">Show All Todos</button>
      <ul v-if="displayAll">
        <!-- Loop through todos array and display each todo -->
        <li v-for="(todo, index) in todos" :key="index">
          {{ todo.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  data() {
    return {
      todo: '',
      editedTodo: null,
      todos: [
        {
          name: 'Altschool Software Engineering.',
        },
        {
          name: 'My Fellow Altschool Students.',
        }
        // Add more todos to the array if you have them
      ],
      displayAll: false // Flag to control displaying all todos
    };
  },
  methods: {
    submitTodo() {
      if (this.todo.length === 0) return;

      if (this.editedTodo === null) {
        this.todos.push({ name: this.todo });
      } else {
        this.todos[this.editedTodo].name = this.todo;
        this.editedTodo = null;
      }

      this.todo = '';
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(index) {
      this.todo = this.todos[index].name;
      this.editedTodo = index;
    },
    showAllTodos() {
      this.displayAll = true; // Show all todos when button is clicked
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

/* Styling for the input section */
.d-flex {
  margin-top: 20px;
  display: flex;
  align-items: center;
}

.form-control {
  flex: 1;
  margin-right: 10px;
}

/* Styling for the table */
.table {
  width: 100%;
}

/* Styling for table headers */
.table th {
  /* text-align: center; */
}

/* Styling for todo rows */
.table td {
  vertical-align: middle;
}

/* Styling for edit and delete icons */
.text-center {
  cursor: pointer;
}

.fa-trash {
  font-size: 18px;
  margin: 0 5px;
}

.fa:hover {
  color: red; /* Change color on hover */
}
</style>
