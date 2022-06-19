<template>
  <div>
    <q-list v-for="item in filteredItems" v-bind:key="item">
      <TodoItem :item="item" :todos="todos" @toggleCheckbox="toggleCheckbox" />
    </q-list>
  </div>
</template>

<script>
import TodoItem from "components/TodoItem.vue";

export default {
  name: "TodosList",
  props: ["todos", "search"],
  computed: {
    categoryItems() {
      const categoryTodoObj = this.todos.filter((item) => {
        return item.categorySelected;
      })[0];
      return categoryTodoObj.items;
    },
    sortedItems() {
      const uncheckedItems = this.categoryItems.filter((item) => {
        return item.checked === false;
      });
      const checkedItems = this.categoryItems.filter((item) => {
        return item.checked === true;
      });
      const sortedItems = uncheckedItems.concat(checkedItems);

      return sortedItems;
    },
    filteredItems() {
      if (this.search !== "") {
        return this.sortedItems.filter((item) => {
          return item.text.toLowerCase().includes(this.search.toLowerCase());
        });
      } else {
        return this.sortedItems;
      }
    },
  },
  components: {
    TodoItem,
  },
  methods: {
    toggleCheckbox(item) {
      this.$emit("toggleCheckbox", item);
    },
  },
};
</script>
