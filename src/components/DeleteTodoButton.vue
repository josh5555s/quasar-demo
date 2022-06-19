<template>
  <q-btn @click="handleButtonClicked"></q-btn>
</template>

<script>
export default {
  props: ["item", "todos"],
  // name: 'ComponentName',
  methods: {
    handleButtonClicked() {
      this.$q
        .dialog({
          title: "Delete Item",
          message: `Are you sure you would like to delete "${this.item.text}" ?`,
          ok: {
            label: "delete",
            color: "negative",
          },
          cancel: {
            color: "primary",
          },
        })
        .onOk(this.deleteAndNotify);
    },
    deleteAndNotify() {
      this.deleteItem();
      this.deletionNotification();
    },
    deletionNotification() {
      this.$q.notify({
        message: `${this.item.text} - deleted!`,
        icon: "mdi-check",
        color: "negative",
      });
    },
    deleteItem() {
      console.log("todos: ", this.todos);
      this.todos.forEach((category) => {
        category.items.forEach((item, i) => {
          if (item.text === this.item.text) {
            category.items.splice(i, 1);
          }
        });
      });
    },
  },
  setup() {
    return {};
  },
};
</script>
