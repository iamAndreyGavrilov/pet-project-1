<template>
  <header class="header">
    <input
      class="header__input shadow"
      :value="filter"
      @input="$emit('update:filter', $event.target.value)"
      type="text"
      placeholder="Поиск"
    />

    <add-button @click="createUser()" />
  </header>
</template>

<script>
import AddButton from "./AddButton.vue";
export default {
  components: {
    AddButton,
  },
  props: {
    filter: String,
  },
  methods: {
    createUser() {
      this.$emit("add-user");
    },
  },
};
</script>

<style scoped>
.header {
  display: flex;
  height: 48px;
}
.header__input {
  width: 100%;
  height: 100%;
  padding: 10px;
}
</style>
