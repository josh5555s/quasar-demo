<template>
  <q-page class="row">
    <q-card class="col-xs-9">
      <q-toolbar>
        <q-input
          dense
          label-slot
          oarderless
          class="full-width"
          v-model="search"
        >
          <template #label>
            {{ searchPlaceholder }}
          </template>
          <template #append>
            <q-icon name="mdi-magnify"></q-icon>
          </template>
        </q-input>
      </q-toolbar>
      <TodosList
        :todos="todos"
        :search="search"
        @toggleCheckbox="toggleCheckbox"
      ></TodosList>
    </q-card>
    <div class="col-xs-3">
      <q-toolbar class="bg-primary">
        <CreateTodoButton
          fab
          color="secondary"
          style="margin-bottom: -44px"
          class="q-ml-md"
          icon="mdi-plus"
          :todos="todos"
        ></CreateTodoButton>
      </q-toolbar>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import CreateTodoButton from "components/CreateTodoButton.vue";
import TodosList from "components/TodosList.vue";

export default defineComponent({
  name: "IndexPage",
  components: {
    CreateTodoButton,
    TodosList,
  },
  props: ["todos"],
  data() {
    return {
      search: "",
    };
  },
  computed: {
    selectedCategory() {
      return this.todos.filter((category) => {
        return category.categorySelected;
      })[0];
    },
    searchPlaceholder() {
      return `Search ${this.selectedCategory.category}`;
    },
  },
  methods: {
    toggleCheckbox(item) {
      this.$emit("toggleCheckbox", item);
    },
  },
});
</script>
