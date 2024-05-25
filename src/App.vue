<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="container">
    <RouterView />

    <footer>
      <div class="menu-container">
        <nav class="menu">
          <RouterLink to="/">Game X2</RouterLink>
          <span>|</span>
          <RouterLink to="/about">Friends</RouterLink>
          <span>|</span>
          <RouterLink to="/earn">Earn</RouterLink>
          <span>|</span>
          <RouterLink to="/boosts">Boosts</RouterLink>
        </nav>
      </div>
    </footer>
  </div>
</template>

<style>
body {
  background: black !important;
  color: white;
  margin: 0;
  transition: 0.01s;
}

.container {
  padding: 0;
  position: relative;
  min-height: 100vh;
}

.menu-container {
  position: absolute;
  display: flex;
  justify-content: center;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: black;
  text-align: center;
  padding: 50px 0;
  z-index: 1000;
}

.menu {
  width: 90%;
  background-color: #ffffff26;
  padding: 1px;
  border-radius: 5px;
  display: flex;
  justify-content: center;

  align-items: center;
  gap: 10px;
}

.menu a {
  text-decoration: none;
  color: #ffffff80;
  padding: 13px;
  font-size: 13px;
}

.menu span {
  color: white;
}
</style>
