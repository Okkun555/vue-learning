<template>
  <button @click="onCountUpClick">+1</button>
  Click Count: {{ state.count }} <br />
</template>

<script>
import { computed, reactive } from "vue";
export default {
  setup() {
    const state = reactive({
      count: 0,
    });

    const onCountUpClick = () => state.count++;
    const tripleNum = computed(() => state.count * 3);

    return {
      state,
      onCountUpClick,
    };
  },
};
</script>