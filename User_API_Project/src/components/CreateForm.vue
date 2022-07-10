<template>
  <div
    class="modal fade show d-block"
    id="createuser"
    tabindex="-1"
    role="dialog"
    aria-labelledby="createuserTitle"
    aria-hidden="true"
  >
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="createuserTitle">
            <strong>Create New User</strong>
          </h5>
          <button
            type="button"
            class="close"
            data-bs-dismiss="modal"
            aria-label="Close"
            @click.prevent="$emit('closeAddForm')"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form>
            <p>
              Name: <span v-text="required.name"> </span>
              <input type="text" v-model="user.name" />
            </p>
            <p>
              Email: <span v-text="required.email"> </span>
              <input type="text" v-model="user.email" />
            </p>
            <p>
              Phone: <span v-text="required.phone"> </span
              ><input type="text" v-model="user.phone" />
            </p>
          </form>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            @click.prevent="$emit('closeAddForm')"
          >
            Close
          </button>
          <button
            type="button"
            class="btn btn-primary"
            @click.prevent="$emit('create', user)"
          >
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * This is create form component.
 * Modal is added to this page
 */

export default {
  name: "CreateForm",
  data() {
    return {
      user: {
        name: "",
        email: "",
        phone: "",
      },
    };
  },
  props: {
    required: Object,
  },
};
</script>
