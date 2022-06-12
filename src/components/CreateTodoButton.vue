<template>
  <q-btn @click="handleButtonClicked" />
</template>

<script>
export default {
  props: ["todos", "selectedCategory"],
  methods: {
    handleButtonClicked() {
      this.$q
        .dialog({
          title: "Create Todo",
          prompt: {
            model: "",
            type: "text",
          },
        })
        .onOk(this.createTodo);
    },
    createTodo(data) {
      this.this.$q.notify({
        message: `${data} - created!`,
        icon: "mdi-check",
        color: "positive",
      });
    },
  },
};
</script>
