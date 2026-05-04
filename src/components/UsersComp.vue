<template>
  <div class="list-card">
    <div class="list-header">
      <h2>👥 Users List</h2>
      <span v-if="users.length > 0" class="count-badge">{{ users.length }}</span>
    </div>
    
    <table v-if="users.length > 0">
      <thead>
        <tr>
          <th>Name</th>
          <th>Age</th>
          <th>Status</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in users" :key="index">
          <td class="name-cell">
            <span class="user-name">{{ user.name }}</span>
          </td>
          <td class="age-cell">{{ user.age }} years</td>
          <td>
            <span class="badge badge-user">Active</span>
          </td>
          <td class="action-cell">
            <button class="delete-button" @click="$emit('delete-user', index)" title="Delete this user">🗑️ Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    
    <div v-else class="empty-state-container">
      <div class="empty-state-icon">👤</div>
      <p class="empty-state">No users have been added yet.</p>
      <p class="empty-state-hint">Create your first user from the form above!</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UsersComp',
  props: {
    users: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style scoped>

</style>
