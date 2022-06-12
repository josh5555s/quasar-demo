<template>
  <a>
    <q-item clickable @click="selectCategory">
      <q-item-section side>
        <q-icon :name="item.icon"></q-icon>
      </q-item-section>
      <q-item-section> {{ item.category }} </q-item-section>
      <q-item-section side> {{ item.items.length }} </q-item-section>
    </q-item>
  </a>
</template>

<script>
export default {
  props: ["item"],
  emits: ["selectCategory"],
  methods: {
    selectCategory() {
      this.$emit("selectCategory", this.item);
    },
  },
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
a {
  color: inherit;
  text-decoration: none;
}
</style>
