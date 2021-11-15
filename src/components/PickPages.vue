<template>
  <div class="footer__right">
    <div class="page__select shadow">
      <select
        class="footer__select"
        v-model="pageNumber"
        @change="$emit('update:page', $event.target.value)"
      >
        <option
          class="option"
          v-for="pageNumber in pageTotal"
          :key="pageNumber"
        >
          {{ pageNumber }}
        </option>
      </select>
      из {{ pageTotal }} страниц
    </div>
    <div class="arrows">
      <button
        class="arrow__btn"
        :disabled="disBtn"
        @click="changeDisabledBack()"
      >
        <img src="@/assets/image/icon__16__pagination-left.png" alt="" />
      </button>
      <button
        class="arrow__btn"
        :disabled="disBtnNext"
        @click="changeDisabledNext()"
      >
        <img src="@/assets/image/icon__16__pagination-right.png" alt="" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pageNumber: 1,
    };
  },
  props: {
    page: {
      type: Number,
      required: true,
    },
    pageTotal: {
      type: Number,
      required: true,
    },
    disBtn: {
      type: Boolean,
      required: true,
    },
    disBtnNext: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    changeDisabledBack() {
      this.$emit("page-back");
    },
    changeDisabledNext() {
      this.$emit("page-next");
    },
  },
  watch: {
    page() {
      this.pageNumber = this.page;
    },
  },
};
</script>

<style scoped>
.footer__right {
  display: flex;
  height: 100%;
}
/* .shadow {
  box-shadow: inset -1px -1px 0px rgba(0, 0, 0, 0.5);
} */
.arrow__btn {
  width: 48px;
  height: 100%;
  cursor: pointer;
}
.arrow__btn:disabled {
  opacity: 0.33;
}
.page__select {
  width: 221px;
  display: flex;
  align-items: center;
  color: #7b8395;
  justify-content: space-evenly;
}
.footer__select {
  width: 79px;
  /* height: 97%; */
  border: none;
  text-align: center;
}
.shadow {
  box-shadow: inset 1px 0px 0px rgba(198, 209, 221, 0.5),
    inset -1px 0px 0px rgba(198, 209, 221, 0.5);
}
</style>
