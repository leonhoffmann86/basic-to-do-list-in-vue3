<template>
  <main>
    <h1>BTTL - <small>Basic To Do List</small></h1>
    <form @submit.prevent="addNewToDo">
      <label for="newTodo">New To Do</label>
      <input v-model="newToDo" type="text" name="newTodo" />
      <button>Add</button>
    </form>
    <section id="todos">
      <ul>
        <li
          :class="{ done: toDo.done }"
          @click="toggleDone(toDo)"
          v-for="toDo in toDos"
          :key="toDo.id"
        >
          {{ toDo.todo }}
        </li>
      </ul>
    </section>

    <hr />

    <section id="done-todos">
      <ul>
        <li
          :class="{ done: toDo.done }"
          @click="toggleUndone(toDo)"
          v-for="toDo in doneToDos"
          :key="toDo.id"
        >
          {{ toDo.todo }}
        </li>
      </ul>
    </section>
  </main>
</template>

<script>
import { ref } from "vue";

export default {
  name: "ToDoList",

  setup() {
    const newToDo = ref("");
    const toDos = ref([]);
    const doneToDos = ref([]);

    function addNewToDo() {
      toDos.value.push({ id: Date.now, done: false, todo: newToDo.value });
      newToDo.value = "";
    }

    function toggleDone(toDo) {
      toDo.done = true;

      var index = toDos.value.indexOf(toDo);
      toDos.value.splice(index, 1);
      doneToDos.value.push(toDo);
    }

    function toggleUndone(toDo) {
      toDo.done = false;

      var index = doneToDos.value.indexOf(toDo);
      doneToDos.value.splice(index, 1);
      toDos.value.push(toDo);
    }

    return {
      newToDo,
      toDos,
      doneToDos,
      addNewToDo,
      toggleDone,
      toggleUndone,
    };
  },
};
</script>

<style scoped>
main {
  width: 100%;
  margin: 0 auto;
}

form,
hr {
  max-width: 100%;
}

input {
  height: 40px;
}

button {
  height: 46px;
}

label {
  margin-right: 10px;
}

li {
  text-align: left;
  cursor: pointer;
  padding: 10px;
}

li:hover,
li:active {
  border: 1px solid lightgray;
  border-radius: 2px;
}

.done {
  text-decoration: line-through;
  color: lightgray;
}

@media (min-width: 600px) {
  main {
    max-width: 800px;
    width: 600px;
  }
  input {
    width: 60%;
  }
}
</style>
