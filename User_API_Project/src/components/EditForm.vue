<template>
<div class="modal fade show d-block" id="updateuser" tabindex="-1" role="dialog" aria-labelledby="updateuserTitle" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="updateuserTitle"><strong>Edit this User</strong></h5>
        <button type="button" class="close"  aria-label="Close" @click.prevent="$emit('closeEditForm')">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <form>
            <p>Name: <span v-text="required.name"> </span> <input type="text" v-model="edituser.name"></p>
            <p>Email: <span v-text="required.email"> </span> <input type="text" v-model="edituser.email"></p>
            <p>Phone: <span v-text="required.phone"> </span><input type="text" v-model="edituser.phone"></p>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" @click.prevent="$emit('closeEditForm')">Close</button>
        <button type="button" class="btn btn-primary" @click.prevent="$emit('update',edituser)">Save changes</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>

/**
 * This is edit form component.
 * Modal is added to this page
 */

export default {
    name: 'EditForm',
    props: {
        user: Object,
        required:Object
    },
    data(){
        return{
            edituser: {... this.user}
        }
    }
}

</script>

<style>

</style>
