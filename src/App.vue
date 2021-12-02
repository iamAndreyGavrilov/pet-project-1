<template>
  <div class="table_wrapper shadow__two">
    <header-table @add-user="createUser" v-model:filter="filter" />
    <table class="fixed">
      <thead class="thead">
        <tr>
          <th class="shadow">Пользователь</th>
          <th class="shadow">Номер телефона</th>
          <th class="shadow">Email</th>
          <th class="shadow">Дата регистрации</th>
          <th class="shadow">Код</th>
          <th class="shadow">Город</th>
          <th class="shadow"></th>
        </tr>
      </thead>
      <tbody class="tbody">
        <tr>
          <td class="tbody__add">
            <input placeholder="Введите имя" v-model="name" type="text" />
          </td>
          <td class="tbody__add"><input v-model="phone" type="text" /></td>
          <td class="tbody__add"><input v-model="email" type="text" /></td>
          <td class="tbody__add"><input v-model="zipcode" type="text" /></td>
          <td class="tbody__add"><input v-model="id" type="text" /></td>
          <td class="tbody__add"><input v-model="city" type="text" /></td>
          <td class="shadow"></td>
        </tr>
      </tbody>
      <tfoot class="tfoot">
        <user-list
          :paginationUsers="paginationUsers"
          @edit-user="editUser"
          @remove-user="removeUser"
          v-model:user.name="user.name"
          v-model:user.phone="user.phone"
          v-model:user.email="user.email"
          v-model:user.address.zipcode="user.address.zipcode"
          v-model:user.id="user.id"
          v-model:user.address.city="user.address.city"
        />
        <!-- <tr style="height: 48px" v-for="user in filteredUsers()" :key="user.id">
          <td style="width: 300px" class="shadow">
            <p v-if="isUserReadonly(user)">{{ user.name }}</p>
            <input
              class="input"
              v-else
              v-model="user.name"
              type="text"
              :readonly="isUserReadonly(user)"
            />
          </td>
          <td style="width: 210" class="shadow">
            <p v-if="isUserReadonly(user)">{{ user.phone }}</p>

            <input
              class="input"
              v-else
              v-model="user.phone"
              type="text"
              :readonly="isUserReadonly(user)"
            />
          </td>
          <td style="width: 350" class="shadow">
            <p v-if="isUserReadonly(user)">{{ user.email }}</p>

            <input
              class="input"
              v-else
              v-model="user.email"
              type="text"
              :readonly="isUserReadonly(user)"
            />
          </td>
          <td style="width: 150px" class="shadow">
            <p v-if="isUserReadonly(user)">{{ user.address.zipcode }}</p>

            <input
              class="input"
              v-else
              v-model="user.address.zipcode"
              type="text"
              :readonly="isUserReadonly(user)"
            />
          </td>
          <td style="width: 100px" class="shadow">
            <p v-if="isUserReadonly(user)">{{ user.id }}</p>

            <input
              class="input"
              v-else
              v-model="user.id"
              type="text"
              :readonly="isUserReadonly(user)"
            />
          </td>
          <td style="width: 250px" class="shadow">
            <p v-if="isUserReadonly(user)">{{ user.address.city }}</p>

            <input
              class="input"
              v-else
              v-model="user.address.city"
              type="text"
              :readonly="isUserReadonly(user)"
            />
          </td>
          <td style="width: 80px">
            <div class="btns">
              <button class="btns__table" @click="editUser(user)">
                <img
                  v-if="isUserReadonly(user)"
                  src="./assets/image/Icons_16_edit.png"
                  alt=""
                />
                <img v-else src="./assets/image/Icons_16_save.png" alt="" />
              </button>
              <button class="btns__table" @click="removeUser(user)">
                <img src="./assets/image/Icons_16_delete.png" alt="" />
              </button>
            </div>
          </td>
        </tr> -->
      </tfoot>
    </table>

    <footer class="footer shadow">
      <settings-display-users
        v-model:currentUser="currentUser"
        v-model:currentUsers="currentUsers"
        v-model:usersAll="usersAll"
        v-model:selected="selected"
      />
      <pick-pages
        v-model:page="page"
        v-model:pageTotal="pageTotal"
        v-model:disBtn="disBtn"
        v-model:disBtnNext="disBtnNext"
        @page-back="changeDisabledBack"
        @page-next="changeDisabledNext"
      />
      <!-- <div class="footer__left">
        <div class="items__user shadow">
          <div id="v-model-select" class="demo">
            <span>Отображать по:</span>
            <select v-model="selected">
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
      </div> -->
      <!-- <div class="footer__right">
        <div class="page__select shadow">
          <select v-model="page">
            <option v-for="pageNumber in pageTotal" :key="pageNumber">
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
            <img src="./assets/image/icon__16__pagination-left.png" alt="" />
          </button>
          <button
            class="arrow__btn"
            :disabled="disBtnNext"
            @click="changeDisabledNext()"
          >
            <img src="./assets/image/icon__16__pagination-right.png" alt="" />
          </button>
        </div>
      </div> -->
    </footer>
  </div>
</template>

<script>
import { fetchUsers } from "./api.js";
import HeaderTable from "./components/HeaderTable.vue";
import SettingsDisplayUsers from "./components/SettingsDisplayUsers.vue";
import PickPages from "./components/PickPages.vue";
import UserList from "./components/UserList.vue";

export default {
  name: "App",
  components: { HeaderTable, SettingsDisplayUsers, PickPages, UserList },
  data() {
    return {
      users: [],
      user: {
        name: "",
        phone: "",
        email: "",
        id: "",
        address: {
          city: "",
          zipcode: "",
        },
      },
      page: 1,
      selected: 5,
      // pageTotal: 0,
      // currentUser: 0,
      // currentUsers: 0,
      // usersAll: 0,
      filter: "",
      disBtn: true,
      // disBtnNext: false,
      // hasNextPage: true,
      // readonlyStatus: true,
      userToEdit: null,
    };
  },
  methods: {
    createUser() {
      const newUser = {
        name: this.name,
        phone: this.phone,
        email: this.email,
        // id: Date.now(),
        id: this.id,
        address: {
          city: this.city,
          zipcode: this.zipcode,
        },
      };
      if (this.name === "") {
        return;
      } else {
        this.users.push(newUser);
      }
      // this.users.push(newUser);
      this.filter = "";
      this.name = "";
      this.phone = "";
      this.email = "";
      this.id = "";
      this.city = "";
      this.zipcode = "";
    },
    removeUser(userToRemove) {
      this.users = this.users.filter((user) => user !== userToRemove);
    },
    editUser(userToEdit) {
      this.userToEdit = userToEdit;
      if (this.userToEdit === null) {
        return true;
      }
    },

    // isUserReadonly(user) {
    //   if (this.userToEdit === null) {
    //     return true;
    //   }
    //   return user.id !== this.userToEdit.id;
    // },

    async getUsers() {
      try {
        this.users = await fetchUsers();
      } catch (error) {
        console.error("Ошибка", error);
      }
    },
    changeDisabledNext() {
      this.page = Number(this.page) + 1;
    },
    changeDisabledBack() {
      this.page = Number(this.page) - 1;
    },
  },
  computed: {
    startIndex() {
      return (this.page - 1) * this.selected;
    },
    endIndex() {
      return this.page * this.selected;
    },
    filteredUsers() {
      return this.users.filter((user) =>
        user.name.toLowerCase().includes(this.filter.toLowerCase())
      );
    },
    paginationUsers() {
      return this.filteredUsers.slice(this.startIndex, this.endIndex);
    },
    hasNextPage() {
      return this.filteredUsers.length > this.endIndex;
    },
    pageTotal() {
      return Math.ceil(this.filteredUsers.length / this.selected);
    },
    currentUser() {
      return this.startIndex + 1;
    },
    currentUsers() {
      return this.endIndex;
    },
    usersAll() {
      return this.filteredUsers.length;
    },
    disBtnNext() {
      return (
        this.filteredUsers.length < this.endIndex ||
        this.filteredUsers.length === this.endIndex
      );
    },
  },
  mounted() {
    this.getUsers();
  },
  watch: {
    filter() {
      this.page = 1;
    },
    selected() {
      this.page = 1;
    },
    page() {
      this.page = Number(this.page);
      if (this.page > 1) {
        this.disBtn = false;
        this.disBtnNext = false;
      } else if (this.page === 1) {
        this.disBtn = true;
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@500&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "IBM Plex Mono", monospace;
  font-style: normal;
  font-weight: 500;
  font-size: 13px;
  line-height: 16px;
}
.table_wrapper {
  margin: 20px auto;
  max-width: 1440px;
  max-height: 744px;
}

.page__wrapper {
  display: flex;
}
.page {
  border: 1px solid red;
  margin: 5px 5px 5px 5px;
  cursor: pointer;
}

.thead {
  height: 48px;
  font-style: normal;
  font-weight: 500;
  font-size: 12px;
  line-height: 16px;
  color: #7b8395;
  background: rgba(219, 221, 223, 0.5);
}

.btns__table {
  width: 40px;
  height: 40px;
}
.fixed {
  width: 100%;
  /* max-height: 648px; */
}
.footer {
  height: 48px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.shadow {
  box-shadow: inset -1px -1px 0px rgba(0, 0, 0, 0.5);
}
.shadow__two {
  box-shadow: -1px -1px 0px rgba(0, 0, 0, 0.5);
}
input {
  border: none;
  width: 99%;
  /* padding: 5px; */
  height: 95%;
}
.input {
  background-color: #afd7ff;
  height: 48px;
}
.tbody {
  height: 48px;
}
.tbody__add {
  border: 1px solid #0080ff;
  height: 40px;
  border-radius: 5px;
}
</style>
