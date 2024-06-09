<script setup></script>

<template>
  <div class="card border-0 rounded shadow-sm">
    <div class="card-header">MAIN MENU</div>
    <div class="card-body">
      <div class="list-group">
        <router-link
          :to="{ name: 'dashboard' }"
          class="list-group-item list-group-item-action"
          >Dashboard</router-link
        >
        <router-link
          :to="{ name: 'admin.users.index' }"
          class="list-group-item list-group-item-action"
          >Users</router-link
        >
        <a href="#" class="list-group-item list-group-item-action">Logout</a>
      </div>
    </div>
  </div>
</template>
