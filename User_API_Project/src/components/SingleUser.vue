<template>

          <tr >
            <td v-text="user.id"></td>
            <td v-text="user.name"></td>
            <td v-text="user.email"></td>
            <td v-text="user.phone"></td>
            <td>
              <button type="button" @click="$emit('edituser', user)" class="btn btn-primary btn-sm">Edit</button>
              <button type="button" @click="$emit('deleteUser', user)" class="btn btn-secondary btn-sm">Delete</button>
            </td>
          </tr>

</template>

<script>

  /**
   * This Component is create to emit Single user.
   */

    export default {
        name: 'SingleUser',
        props: 
        {
            user: Object
        }
    }

</script>

<style>

</style>
