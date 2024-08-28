<template>
  <section class="add-todo">
    <form
        v-if="isVisibleForm"
        class="add-todo__form"
        @submit.prevent="addTodo"
    >
      <button class="close-button" type="button" @click="unVisibleForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="nameTodo" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="visibleForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import {ITodo} from "@/types/todo";

interface State {
  isVisibleForm: boolean,
  nameTodo: string
}
export default defineComponent({
  data(): State {
    return {
      isVisibleForm: false,
      nameTodo: ''
    }
  },
  methods: {
    visibleForm() {
      this.isVisibleForm = true
    },
    unVisibleForm() {
      this.isVisibleForm = false
    },
    addTodo() {
      this.$emit('addTodo', { id: Date.now(), title: this.nameTodo, status: false })
      this.nameTodo = ''
    }
  },
  emits: {
    addTodo: (todo: ITodo) => todo
  }
})
</script>