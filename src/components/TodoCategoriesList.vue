<template>
  <q-list v-for="item in todos" v-bind:key="item.category">
    <TodoCategory :item="item" @selectCategory="selectCategory" />
  </q-list>
</template>

<script>
import TodoCategory from "components/TodoCategory.vue";

export default {
  props: ["todos"],
  emit: ["selectCategory"],
  components: {
    TodoCategory,
  },
  methods: {
    selectCategory(item) {
      this.$emit("selectCategory", item);
    },
  },
  created() {
    console.log(this.todos);
  },
  setup() {
    return {};
  },
};
</script>
