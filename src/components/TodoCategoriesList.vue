<template>
  <div>
    <q-list v-for="item in todos" v-bind:key="item.category">
      <TodoCategory :item="item" @selectCategory="selectCategory" />
    </q-list>
  </div>
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
    }
  }
};
</script>
