<template>
  <li class="todo-item" :class="{ done: done }" @click="handleClick">
    <span v-if="done">✔︎</span>
    <slot />
  </li>
</template>

<script>
export default {
  props: {
    done: {
      type: Boolean,
    },
  },
  emits: ["toggle"],
  methods: {
    handleClick() {
      this.$emit("toggle");
    },
  },
};
</script>

