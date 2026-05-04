<template>
  <div class="list-card">
    <div class="list-header">
      <h2>🔑 Admins List</h2>
      <span v-if="admins.length > 0" class="count-badge">{{ admins.length }}</span>
    </div>
    
    <table v-if="admins.length > 0">
      <thead>
        <tr>
          <th>Name</th>
          <th>Age</th>
          <th>Status</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(admin, index) in admins" :key="index">
          <td class="name-cell">
            <span class="admin-name">{{ admin.name }}</span>
          </td>
          <td class="age-cell">{{ admin.age }} years</td>
          <td>
            <span class="badge badge-admin">Admin</span>
          </td>
          <td class="action-cell">
            <button class="delete-button" @click="$emit('delete-admin', index)" title="Delete this admin">🗑️ Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    
    <div v-else class="empty-state-container">
      <div class="empty-state-icon">🔐</div>
      <p class="empty-state">No admins have been added yet.</p>
      <p class="empty-state-hint">Create your first admin from the form above!</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AdminsComp',
  props: {
    admins: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style scoped>

</style>
