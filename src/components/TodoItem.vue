<template>
  <q-item>
    <q-item-section side>
      <q-checkbox @click="toggleCheckbox" :model-value="item.checked">
      </q-checkbox>
    </q-item-section>
    <q-item-section>{{ item.text }}</q-item-section>
    <q-item-section side>
      <DeleteTodoButton
        flat
        round
        size="sm"
        icon="mdi-delete"
      ></DeleteTodoButton>
    </q-item-section>
  </q-item>
</template>

<script>
import DeleteTodoButton from "components/DeleteTodoButton.vue";
export default {
  components: {
    DeleteTodoButton,
  },
  props: ["item"],
  emits: ["toggleCheckbox"],
  methods: {
    toggleCheckbox() {
      this.$emit("toggleCheckbox", this.item);
    },
  },

  setup() {
    return {};
  },
};
</script>
