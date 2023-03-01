<template>
  <div>
    <select v-model="selectedUser">
      <option v-for="user,index in users" :key="index" :value="user">{{ user.name }}</option>
    </select>
    <input type="text" v-model="newUserName">
    <button @click="addUser">Add User</button>
    <button @click="updateUser">Update User</button>
    <button @click="deleteUser">Delete User</button>
  </div>
</template>

<script>
export default {
  props: {
    users: Array,
    selectedUser: Object,
    newUserName: String,
    addUser: Function,
    updateUser: Function,
    deleteUser: Function
  }
}
</script>
