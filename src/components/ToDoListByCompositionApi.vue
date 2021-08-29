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
</template>

<script>
import { ref, reactive, computed } from "vue";

// function useTextFilter(items, getItemText) {
//   const filterValue = ref("");
//   const filteredItems = computed(() => {
//     if (!filterValue.value) {
//       return items;
//     }
//     return items.filter((item = getItemText(item).includes(filterValue.value)));
//   });

//   return {
//     filterValue,
//     filteredItems,
//   };
// }

export default {
  setup() {
    // 元となるTODOリスト
    const todoItems = reactive([
      { id: 1, text: "海に行く", done: false },
      { id: 2, text: "山に行く", done: false },
    ]);

    const inputValue = ref("");
    const handleClick = () => {
      const id = todoItems.length + 1;
      todoItems.push({ id, text: inputValue.value, done: false });
      inputValue.value = "";
    };

    // TODOリストの絞り込み関連の定義;
    const filterValue = ref("");
    const filteredTodoItems = computed(() => {
      if (!filterValue.value) {
        return todoItems;
      }
      return todoItems.filter((todo) => todo.text.includes(filterValue.value));
    });

    // const { filterValue, filteredItems: filteredTodoItems } = useTextFilter(
    //   todoItems,
    //   (todo) => todo.text
    // );

    return {
      inputValue,
      filterValue,
      filteredTodoItems,
      handleClick,
    };
  },
};
</script>