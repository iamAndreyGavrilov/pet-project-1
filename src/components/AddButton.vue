<template>
  <button class="header__button">
    <img
      class="button__img plus"
      src="../assets/image/Icons_16_plusWhite.png"
      alt=""
    />
    Добавить пользователя
  </button>
</template>

<script>
export default {};
</script>

<style scoped>
.header__button {
  display: flex;
  align-items: center;
  width: 225px;
  height: 100%;
  background-color: #316bff;
  color: white;
  justify-content: space-between;
  padding: 3px;
}
.header__button:hover {
  background-color: #1049dc;
  cursor: pointer;
}
.button__img.plus {
  height: 16px;
  width: 16px;
}
</style>
