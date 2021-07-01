<template>
  <main>
    <h1>BTTL - <small>Basic To Do List</small></h1>
    <form @submit.prevent="addNewToDo">
      <label for="newTodo">New To Do</label>
      <input v-model="newToDo" type="text" name="newTodo" />
      <button>Add</button>
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
    </form>
  </main>
</template>

<script>
import { ref } from "vue";

export default {
  name: "ToDoList",

  setup() {
    const newToDo = ref("");
    const toDos = ref([]);

    function addNewToDo() {
      toDos.value.push({ id: Date.now, done: false, todo: newToDo.value });
      newToDo.value = "";
    }

    function toggleDone(toDo) {
      toDo.done = !toDo.done;
    }

    return {
      newToDo,
      toDos,
      addNewToDo,
      toggleDone,
    };
  },
};
</script>

<style scoped>
main {
  width: 600px;
  margin: 0 auto;
}

@media (max-width: 600px) {
  main {
    width: 100%;
  }
}

input {
  min-width: 160px;
  max-width: 80%;
}

label {
  margin-right: 10px;
}

li {
  text-align: left;
  cursor: pointer;
}

.done {
  text-decoration: line-through;
  color: lightgray;
}
</style>
