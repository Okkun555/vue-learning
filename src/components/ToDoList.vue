<template>
  <input type="text" v-model="inputValue" />
  <button @click="handleClick">入力した内容を表示</button>
  <div>
    <input v-model="filterValue" placeholder="フィルタテキスト" />
  </div>
  <ul>
    <li
      v-for="todo in filteredTodoItems"
      v-bind:key="todo.id"
      class="todo-item"
      :class="{ done: todo.done }"
      @click="todo.done = !todo.done"
    >
      <span v-if="todo.done">✔︎</span>
      {{ todo.text }}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "",
      filterValue: "",
      todoItems: [
        { id: 1, text: "海に行く", done: false },
        { id: 2, text: "山に行く", done: false },
      ],
    };
  },
  computed: {
    filteredTodoItems() {
      if (!this.filterValue) {
        return this.todoItems;
      }

      return this.todoItems.filter((todo) => {
        return todo.text.includes(this.filterValue);
      });
    },
  },
  methods: {
    handleClick() {
      this.todoItems.push({
        id: this.todoItems.length + 1,
        text: this.inputValue,
        done: false,
      });

      this.inputValue = "";
    },
  },
};
</script>

<style scoped>
.todo-item.done {
  background-color: #3fb983;
  color: #ffffff;
}
</style>