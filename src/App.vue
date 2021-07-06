<template>

  <nav>
    <div class="container">
      <div class="nav-list">
        <router-link to="/" class="routerLink">Home</router-link> 
        <router-link to="/todos" class="routerLink">Todos</router-link>
      </div>
    </div>
  </nav>
  <router-view />
  
</template>

