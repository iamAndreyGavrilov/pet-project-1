<template>
  <div class="footer__left">
    <div class="items__user shadow">
      <div id="v-model-select" class="demo">
        <span>Отображать по:</span>
        <select
          class="footer__select"
          @change="$emit('update:selected', $event.target.value)"
        >
          <option>5</option>
          <option>10</option>
          <option>20</option>
          <option>50</option>
          <option>100</option>
        </select>
      </div>
    </div>

    <div class="page__view shadow">
      {{ currentUser }}-{{ currentUsers }} из {{ usersAll }} пользователей
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentUser: {
      type: Number,
      required: true,
    },
    currentUsers: {
      type: Number,
      required: true,
    },
    usersAll: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.footer__left {
  display: flex;
  height: 100%;
  width: 457px;
}
.items__user {
  width: 215px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.page__view {
  height: 100%;
  width: 242px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  color: #7b8395;
}
.footer__select {
  width: 79px;
  /* height: 97%; */
  border: none;
  text-align: center;
}
/* .shadow {
  box-shadow: inset -1px -1px 0px rgba(0, 0, 0, 0.5);
} */
</style>
