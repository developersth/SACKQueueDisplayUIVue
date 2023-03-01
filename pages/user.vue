<template>
  <div>
    <user-list
      :users="users"
      :editUser="editUser"
      :deleteUser="deleteUser"
    ></user-list>
    <user-select
      :users="users"
      :selectedUser="selectedUser"
      :newUserName="newUserName"
      :addUser="addUser"
      :updateUser="updateUser"
      :deleteUser="deleteUser"
    ></user-select>
  </div>
</template>
  
  <script>
import UserList from '../components/UserList.vue'
import UserSelect from '../components/UserSelect.vue'

export default {
  components: {
    UserList,
    UserSelect,
  },
  data() {
    return {
      users: [
        { id: 1, name: 'John' },
        { id: 2, name: 'Jane' },
        { id: 3, name: 'Cristino' },
      ],
      selectedUser: null,
      newUserName: '',
    }
  },
  methods: {
    editUser(user) {
      this.selectedUser = user
      this.newUserName = user.name
    },
    deleteUser(user) {
      const index = this.users.indexOf(user)
      if (index !== -1) {
        this.users.splice(index, 1)
      }
      if (this.selectedUser === user) {
        this.selectedUser = null
        this.newUserName = ''
      }
    },
    addUser() {
      const id = this.users.length + 1
      const user = { id, name: this.newUserName }
      this.users.push(user)
      this.selectedUser = user
      this.newUserName = ''
    },
    updateUser() {
      if (this.selectedUser) {
        this.selectedUser.name = this.newUserName
      }
      this.selectedUser = null
      this.newUserName = ''
    },
  },
}
</script>
  