<template>
  <div>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }} <button @click="editUser(user)">Edit</button> <button @click="deleteUser(user)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    users: Array,
    editUser: Function,
    deleteUser: Function
  }
}
</script>