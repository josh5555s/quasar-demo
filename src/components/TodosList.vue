<template>
  <q-list v-for="item in categoryItems" v-bind:key="item">
    <TodoItem :item="item" @toggleCheckbox="toggleCheckbox" />
  </q-list>
</template>

<script>
import TodoItem from "components/TodoItem.vue";

export default {
  name: "TodosList",
  props: ["todos"],
  computed: {
    categoryItems() {
      const categoryTodoObj = this.todos.filter((item) => {
        return item.categorySelected;
      })[0];
      return categoryTodoObj.items;
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
  created() {
    console.log(this.categoryItems);
  },
};
</script>
