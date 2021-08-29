<template>
  <input type="text" v-model="inputValue" />
  <button @click="handleClick">入力した内容を表示</button>
  <div>
    <input v-model="filterValue" placeholder="フィルタテキスト" />
  </div>
  <ul>
    <ToDoItem
      v-for="todo in filteredTodoItems"
      :key="todo.id"
      :done="todo.done"
      v-on:toggle="todo.done = !todo.done"
    >
      <b>{{ todo.text }}</b>
    </ToDoItem>
  </ul>

  <button @click="show = !show">表示切り替え</button>
  <transition name="fade">
    <div v-if="show">Awesome Transition</div>
  </transition>
</template>

<script>
import ToDoItem from "./ToDoItem.vue";

export default {
  components: { ToDoItem },
  data() {
    return {
      inputValue: "",
      filterValue: "",
      todoItems: [
        { id: 1, text: "海に行く", done: false },
        { id: 2, text: "山に行く", done: false },
      ],
      show: true,
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1000ms ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>