<template>
  <AppHeader />
  <AppFilter
      :active-filter="activeFilter"
      @switch-filter="switchFilter"
  />

  <main>
    <AppTodoList
        :todos="filteredTodos"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo"
    />
    <AppAddTodo @add-todo="addTodo" />
  </main>
  <AppFooter :statistics="checkStatistics"/>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import AppHeader from "@/components/AppHeader.vue";
import AppFilter from "@/components/AppFilter.vue";
import AppTodoList from "@/components/AppTodoList.vue";
import AppAddTodo from "@/components/AppAddTodo.vue";
import AppFooter from "@/components/AppFooter.vue";
import {ITodo} from "@/types/todo";
import {FilterType} from "@/types/filter";
import {Statistics} from "@/types/statistics";

interface State {
  todos: ITodo[],
  activeFilter: FilterType
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
      ],
      activeFilter: 'All'
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
    },
    switchFilter(filter: FilterType) {
      this.activeFilter = filter
    }
  },
  computed: {
    filteredTodos(): ITodo[] {
      switch (this.activeFilter) {
        case "Active":
          return this.activeTodo
        case "Done":
          return this.doneTodo
        case "All":
        default:
          return this.todos
      }
    },
    checkStatistics(): Statistics {
      return {
        active: this.activeTodo.length,
        done: this.doneTodo.length
      }
    },
    activeTodo(): ITodo[] {
      return this.todos.filter(todo => !todo.status)
    },
    doneTodo(): ITodo[] {
      return this.todos.filter(todo => todo.status)
    }
  }
})
</script>