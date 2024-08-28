<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
          v-for="filter in filtersArr"
          :key="filter"
          class="button"
          :class="{'button--primary': activeFilter === filter}"
          @click="switchFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {FilterType} from "@/types/filter";

interface State {
  filtersArr: FilterType[];
}
export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<FilterType>,
      required: true
    }
  },
  data(): State {
    return {
      filtersArr: ['All', 'Active', 'Done']
    }
  },
  methods: {
    switchFilter(filter: FilterType) {
      this.$emit('switchFilter', filter)
    }
  },
  emits: {
    switchFilter: (filter: FilterType) => filter
  }
})
</script>