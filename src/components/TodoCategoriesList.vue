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
  setup(context) {

    console.log(this.todos);

    function selectCategory(item) {
      context.emit("selectCategory", item);
    }
    return {selectCategory,};
  },
};
</script>
