<template>
  <tr v-for="user in paginationUsers" :key="user.id">
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.name }}</p>

      <input
        class="input"
        v-else
        v-model="userToEdit.name"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.phone }}</p>

      <input
        class="input"
        v-else
        v-model="userToEdit.phone"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.email }}</p>

      <input
        class="input"
        v-else
        v-model="userToEdit.email"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.address.zipcode }}</p>

      <input
        class="input"
        v-else
        v-model="userToEdit.address.zipcode"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.id }}</p>

      <input
        class="input"
        v-else
        v-model="userToEdit.id"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td class="shadow">
      <p v-if="isUserReadonly(user)">{{ user.address.city }}</p>

      <input
        class="input"
        v-else
        v-model="userToEdit.address.city"
        type="text"
        :readonly="isUserReadonly(user)"
      />
    </td>
    <td>
      <div class="btns">
        <button
          v-if="isUserReadonly(user)"
          class="btns__table"
          @click="editUser(user)"
        >
          <img src="@/assets/image/Icons_16_edit.png" alt="" />
        </button>
        <button v-else class="btns__table" @click="saveUser()">
          <img src="@/assets/image/Icons_16_save.png" alt="" />
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
  data() {
    return {
      userToEdit: {
        name: "",
        phone: "",
        email: "",
        id: "",
        address: {
          city: "",
          zipcode: "",
        },
      },
    };
  },
  props: {
    paginationUsers: {
      type: Object,
      required: true,
    },
  },
  methods: {
    removeUser(user) {
      this.$emit("remove-user", user);
    },
    editUser(userToEdit) {
      this.userToEdit = userToEdit;
    },
    saveUser() {
      this.$emit("save-user", this.userToEdit);
      this.userToEdit = null;
    },
    isUserReadonly(user) {
      if (this.userToEdit === null) {
        return true;
      }
      return user.id !== this.userToEdit.id;
    },
  },
};
</script>

<style scoped></style>
