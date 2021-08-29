<template>
  <ToDoList />
  <ToDoListForCompositionApi />
</template>

<script>
import ToDoList from "./components/ToDoList.vue";
import ToDoListForCompositionApi from "./components/ToDoListByCompositionApi.vue";

export default {
  name: "App",
  components: {
    ToDoList,
    ToDoListForCompositionApi,
  },
};
</script>
