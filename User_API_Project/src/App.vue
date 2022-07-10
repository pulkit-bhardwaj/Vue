<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <a class="navbar-brand" href="#">User API CRUD</a>
    </nav>
    <p v-if="success_msg" class="p-2 text-light bg-success">
      {{ success_message }}
    </p>
    <p v-if="error_msg" class="p-2 text-light bg-error">{{ error_message }}</p>
    <button
      type="button"
      class="btn btn-success"
      id="buttonsize"
      @click="openAddDialog"
    >
      Create new User
    </button>
    <div id="tablesize">
      <ListUser
        :users="users"
        @edituser="edituser"
        @deleteUser="deleteUser"
      ></ListUser>
    </div>
    <CreateForm
      v-if="showCreateForm"
      @create="submitUser"
      :required="required"
      @resetError="resetError"
      @closeAddForm="closeAddForm"
    />
    <EditForm
      v-if="showEditForm"
      @update="submitUser"
      @closeEditForm="closeEditForm"
      :user="user"
      :required="required"
    />
  </div>
</template>

<script>
/**
 * 3 Components loaded
 *
 * CreateForm
 * EditForm
 * ListUser
 *
 */

import CreateForm from "./components/CreateForm.vue";
import EditForm from "./components/EditForm.vue";
import ListUser from "./components/ListUser.vue";

/**
 * -----METHODS------
 *
 * edituser(user)
 * - This is use to edit user information with the help of form in EditForm Component.
 *
 * getAllUsers()
 * - This is use to get All users from user_api file provided. Which is currently running on port 8001.
 *
 * submitUser(user)
 * - This is use to submit user from both CreateForm and EditForm used above.
 *
 * deleteUser(user)
 * - This is use to delete user when button is clicked.
 *
 */

export default {
  name: "App",
  components: {
    CreateForm,
    EditForm,
    ListUser,
  },

  data() {
    return {
      api_url: "http://localhost:8001",
      error: false,
      users: [],
      user: {
        name: "",
        email: "",
      },
      showCreateForm: false,
      showEditForm: false,
      error_msg: false,
      success_msg: false,
      error_message: "",
      success_message: "",
      required: {
        name: "",
        email: "",
        phone: "",
      },
    };
  },
  created() {
    this.getAllUsers();
  },
  methods: {
    resetError() {
      this.required = {
        name: "",
        email: "",
        phone: "",
      };
    },
    openAddDialog() {
      this.showCreateForm = true;
      this.resetError();
    },
    closeAddForm() {
      this.showCreateForm = false;
      this.resetError();
    },
    closeEditForm() {
      this.showEditForm = false;
      this.resetError();
      this.user = {};
    },
    edituser(user) {
      this.resetError();
      this.showEditForm = true;
      this.user = { ...user };
    },
    getAllUsers() {
      fetch("http://localhost:8001")
        .then((resp) => resp.json())
        .then((json) => {
          this.users = json.results;
        });
    },
    submitUser(user) {
      if (user.name.length == 0) {
        this.required.name = "Name is Required";
      }
      if (user.email.length == 0) {
        this.required.email = "Email is Required";
      }
      if (user.phone.length == 0) {
        this.required.phone = "Phone is Required";
      }

      if (
        !this.required.name.length &&
        !this.required.email.length &&
        !this.required.phone.length
      ) {
        var method = "";
        if (!user.id) {
          method = "POST";
        } else {
          method = "PUT";
        }
        console.log(method);
        fetch("http://localhost:8001", {
          method: method,
          body: JSON.stringify(user),
          headers: {
            "Content-Type": "application/json",
          },
        })
          .then((resp) => resp.json())
          .then((json) => {
            if (json.status == 200 || json.status == 201) {
              this.showEditForm = false;
              this.showCreateForm = false;
              this.success_msg = true;
              this.success_message = json.message;
            } else {
              this.error_msg = true;
              this.error_message = json.message;
            }
            console.log(json);
            this.getAllUsers();
          });
      }
    },
    deleteUser(user) {
      if (confirm("Are you sure you want to delete this user?")) {
        fetch("http://localhost:8001/?id=" + user.id, {
          method: "DELETE",
          body: JSON.stringify(user),
          headers: {
            "Content-Type": "application/json",
          },
        })
          .then((resp) => resp.json())
          .then((json) => {
            if (json.status == 200 || json.status == 201) {
              console.log(json);
              this.getAllUsers();
              this.success_msg = true;
              this.success_message = json.message;
            } else {
              this.error_msg = true;
              this.error_message = json.message;
            }
          });
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
#tablesize {
  width: 60%;
  text-align: center;
  margin-left: 20%;
  margin-top: 1%;
}
#buttonsize {
  margin-left: -50%;
  margin-top: 5%;
}
.btn-group-sm > .btn,
.btn-sm {
  margin: 2%;
}
</style>
