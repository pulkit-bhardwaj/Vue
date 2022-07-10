<template>
  <table class="table table-striped table-dark">
    <thead>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Name</th>
        <th scope="col">Email</th>
        <th scope="col">Phone</th>
        <th scope="col">Action</th>
      </tr>
    </thead>
    <tbody>
      <SingleUser
        v-for="user in users.slice().reverse()"
        :key="user.user_id"
        :user="user"
        @edituser="$emit('edituser', $event)"
        @deleteUser="$emit('deleteUser', $event)"
      />
    </tbody>
  </table>
</template>

<script>
/**
 * This component is created to List each user.
 */

import SingleUser from "./SingleUser.vue";

export default {
  name: "ListUser",
  props: {
    users: Object,
  },
  components: { SingleUser },
};
</script>

<style>
</style>
