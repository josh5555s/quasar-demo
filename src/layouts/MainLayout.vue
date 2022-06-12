<template>
  <q-layout view="hHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="mdi-menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <q-btn flat round icon="mdi-logout"></q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-toolbar class="bg-primary"></q-toolbar>
      <q-item class="bg-gray-3">
        <q-item-section> Lists </q-item-section>
        <q-section side>
          <CreateTodoListButton
            icon="mdi-plus"
            color="purple"
            flat
            round
            size="sm"
          />
        </q-section>
      </q-item>
      <TodoCategoriesList :todos="todos" @selectCategory="selectCategory" />
    </q-drawer>

    <q-page-container>
      <router-view :todos="todos" @toggleCheckbox="toggleCheckbox" />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import CreateTodoListButton from "components/CreateTodoListButton.vue";
import TodoCategoriesList from "components/TodoCategoriesList.vue";

export default defineComponent({
  name: "MainLayout",
  components: {
    CreateTodoListButton,
    TodoCategoriesList,
  },
  data() {
    return {
      todos: [
        {
          category: "Travel",
          categorySelected: true,
          icon: "mdi-airplane",
          items: [
            {
              text: "Visit Canada",
              checked: false,
            },
            {
              text: "Go camping",
              checked: false,
            },
            {
              text: "Go to the beach",
              checked: false,
            },
          ],
        },
        {
          category: "Shopping",
          categorySelected: false,
          icon: "mdi-shopping",
          items: [
            {
              text: "Buy a paisley shirt",
              checked: false,
            },
            {
              text: "Buy a cargo rack for the car",
              checked: false,
            },
          ],
        },
      ],
    };
  },
  methods: {
    selectCategory(item) {
      const todo = this.todos.filter((todo) => {
        todo.categorySelected = false;
        return todo.category === item.category;
      })[0];
      todo.categorySelected = true;
    },
    toggleCheckbox(toggledItem) {
      const todo = this.todos.filter((todo) => {
        return todo.categorySelected;
      })[0];
      const itemToUpdate = todo.items.filter((possibleItem) => {
        return possibleItem.text === toggledItem.text;
      })[0];
      itemToUpdate.checked = !itemToUpdate.checked;
    },
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
