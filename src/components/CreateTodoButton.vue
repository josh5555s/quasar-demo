<template>
  <q-btn @click="handleButtonClicked" />
</template>

<script>
export default {
  data() {
    return {
      textInput: "",
    };
  },
  props: ["todos", "selectedCategory"],
  methods: {
    handleButtonClicked() {
      this.$q
        .dialog({
          title: "Create New Todo Item",
          prompt: {
            type: "text",
          },
        })
        .onOk(this.createAndNotify);
    },
    createAndNotify(data) {
      if (data !== undefined) {
        this.textInput = data;
        this.createItem();
        this.creationNotification();
      }
    },
    createItem() {
      console.log("todos: ", this.todos);
      this.todos.forEach((category) => {
        if (category.categorySelected) {
          category.items.unshift({
            text: this.textInput,
            checked: false,
          });
        }
      });
    },
    creationNotification() {
      this.$q.notify({
        message: `${this.textInput} - created!`,
        icon: "mdi-check",
        color: "positive",
      });
    },
  },
};
</script>
