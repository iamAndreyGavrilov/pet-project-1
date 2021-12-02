<template>
  <tr v-for="user in paginationUsers" :key="user.id">
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.name }}</p>

      <input
        class="input"
        v-else
        :value="user.name"
        @input="$emit('update:user.name', $event.target.value)"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.phone }}</p>

      <input
        class="input"
        v-else
        :value="user.phone"
        @input="$emit('update:user.phone', $event.target.value)"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.email }}</p>

      <input
        class="input"
        v-else
        :value="user.email"
        @input="$emit('update:user.email', $event.target.value)"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.address.zipcode }}</p>

      <input
        class="input"
        v-else
        :value="user.address.zipcode"
        @input="$emit('update:user.address.zipcode', $event.target.value)"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.id }}</p>

      <input
        class="input"
        v-else
        :value="user.id"
        @input="$emit('update:user.id', $event.target.value)"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.address.city }}</p>

      <input
        class="input"
        v-else
        :value="user.address.city"
        @input="$emit('update:user.address.city', $event.target.value)"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td>
      <div class="btns">
        <button class="btns__table" @click="editUser(user)">
          <img
            v-if="isUserReadonly(user)"
            src="@/assets/image/Icons_16_edit.png"
            alt=""
          />
          <img v-else src="@/assets/image/Icons_16_save.png" alt="" />
        </button>
        <button class="btns__table" @click="removeUser(user)">
          <img src="@/assets/image/Icons_16_delete.png" alt="" />
        </button>
      </div>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    paginationUsers: {
      type: Object,
      required: true,
    },
    isUserReadonly: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    editUser() {
      this.$emit("edit-user", this.user);
    },
    removeUser() {
      this.$emit("remove-user", this.user);
    },
    // isUserReadonly() {
    //   return true;
    // },
  },
};
</script>

<style scoped></style>
