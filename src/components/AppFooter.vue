<template>
  <footer class="app-footer">{{ statistics.active }} more to do, {{ statistics.done }} done</footer>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {Statistics} from "@/types/statistics";


export default defineComponent({
  props: {
    statistics: {
      type: Object as PropType<Statistics>
    }
  }
})
</script>