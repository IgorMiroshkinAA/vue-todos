<template>
  <AppHeader />
  <AppFilter />

  <main>
    <AppTodoList
        :todos="todos"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo"
    />
    <AppAddTodo @add-todo="addTodo" />
  </main>
  <AppFooter />
</template>

<script lang="ts">
import {defineComponent} from "vue";
import AppHeader from "@/components/AppHeader.vue";
import AppFilter from "@/components/AppFilter.vue";
import AppTodoList from "@/components/AppTodoList.vue";
import AppAddTodo from "@/components/AppAddTodo.vue";
import AppFooter from "@/components/AppFooter.vue";
import {ITodo} from "@/types/todo";

interface State {
  todos: ITodo[]
}

export default defineComponent({
  components: {
    AppFooter,
    AppAddTodo,
    AppTodoList,
    AppFilter,
    AppHeader
  },
  data(): State {
    return {
      todos: [
        {
          id: 0, title: 'some text', status: true
        }
      ]
    }
  },
  methods: {
    addTodo(todo: ITodo) {
      this.todos.push(todo)
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find(todo => todo.id === id)

      if (targetTodo) {
        targetTodo.status = !targetTodo.status
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    }
  }
})
</script>