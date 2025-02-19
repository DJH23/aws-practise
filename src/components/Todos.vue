<script setup lang="ts">
import "@/assets/main.css";
import { onMounted, onUnmounted, ref } from "vue";
import type { Schema } from "../../amplify/data/resource";
import { generateClient } from "aws-amplify/data";

// provide a default export name for Vetur
defineOptions({ name: "Todos" });

const client = generateClient<Schema>();

// create a reactive reference to the array of todos
const todos = ref<any[]>([]);
let subscription: { unsubscribe: () => void };

onMounted(() => {
  // subscribe once on mount
  subscription = client.models["Todo"].observeQuery().subscribe({
    next: ({ items, isSynced }) => {
      todos.value = items;
    },
  });
});

onUnmounted(() => {
  subscription && subscription.unsubscribe();
});

function createTodo() {
  const content = window.prompt("Todo content");
  if (!content) return;
  client.models["Todo"].create({ content }).then(() => {
    // no need to call listTodos; subscription handles updates
  });
}

function deleteTodo(id: string) {
  client.models["Todo"].delete({ id });
  // deletion will trigger subscription update
}
</script>

<template>
  <main>
    <h1>My todos</h1>
    <button @click="createTodo">+ new</button>
    <ul>
      <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
        {{ todo.content }}
      </li>
    </ul>
    <div>
      🥳 App successfully hosted. Try creating a new todo.
      <br />
      <a
        href="https://docs.amplify.aws/gen2/start/quickstart/nextjs-pages-router/"
      >
        Review next steps of this tutorial.
      </a>
    </div>
  </main>
</template>
