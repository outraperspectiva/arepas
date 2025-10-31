<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue'
const count = ref(0)

function increment() {
  count.value++
}

let id = 0
const newTodo = ref('')
const todos = ref([])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

const selected = ref('')
</script>

<template>
  <header>
    <img alt="Arepa" class="logo" src="@/assets/arepas.png" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="Primeira Página!" />
      <h4>Selecione a Bebida</h4>
      <select v-model="selected">
        <option disabled value="Refrigerante">Selecione</option>
        <option>Refrigerante</option>
        <option>Água</option>
        <option>Cerveja</option>
      </select>
      <p>{{ selected }}</p>
      <button @click="increment">Quantidade: {{ count }}</button>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" required placeholder="Item do Pedido" />
        <button>Adicionar a Lista de Pedidos</button>
      </form>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          {{ todo.text }}
          <button @click="removeTodo(todo)">X</button>
        </li>
      </ul>

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">Pedidos</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
