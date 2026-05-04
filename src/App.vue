<template>
  <div class="app-shell">
    <header class="app-header">
      <h1>Vue 3 Options API User/Admin Manager</h1>
      <p>Use the form to add people and switch between user/admin lists.</p>
    </header>

    <div class="button-group">
      <button :class="{ active: currentView === 'form' }" @click="currentView = 'form'">Form View</button>
      <button :class="{ active: currentView === 'users' }" @click="currentView = 'users'">Users List</button>
      <button :class="{ active: currentView === 'admins' }" @click="currentView = 'admins'">Admins List</button>
    </div>

    <section class="content-card">

      <div v-if="currentView === 'form'" class="form-card">
        <h2>Add New Person</h2>
        <form @submit.prevent="submitForm">
                                          <label>Name<input v-model.trim="form.name" type="text" placeholder="Enter name" /></label>
<br>
<br>
                                          <label>Age<input v-model.number="form.age" type="number" min="1" placeholder="Enter age" /></label>
<br>
<br>
                                          <label>Role<select v-model="form.role">
<br>
<br>
                                          <option value="user">user</option>
                                          <option value="admin">admin</option></select></label>
<br>
<br>
                                          <button type="submit" class="submit-button">Add {{ form.role }}</button></form>
      </div>

      <UsersComp
        v-else-if="currentView === 'users'"
        :users="users"
        @delete-user="deleteUser"
      />

      <AdminsComp
        v-else-if="currentView === 'admins'"
        :admins="admins"
        @delete-admin="deleteAdmin"
      />
    </section>
  </div>
</template>

<script>
import UsersComp from './components/UsersComp.vue'
import AdminsComp from './components/AdminsComp.vue'

export default {
  name: 'App',
  components: {
    UsersComp,
    AdminsComp,
  },
  data() {
    return {
      form: {
        name: '',
        age: null,
        role: 'user',
      },
      users: [],
      admins: [],
      currentView: 'form',
    }
  },
  methods: {
    submitForm() {
      if (!this.form.name || !this.form.age) {
        alert('Please fill in both name and age before submitting.')
        return
      }

      const newPerson = {
        name: this.form.name,
        age: this.form.age,
      }

      if (this.form.role === 'admin') {
        this.admins.push(newPerson)
        this.currentView = 'admins'
      } else {
        this.users.push(newPerson)
        this.currentView = 'users'
      }   
    },
  },
}
</script>

<style>

</style>
