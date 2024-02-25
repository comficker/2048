<script setup lang="ts">
import {RouterLink, RouterView} from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink class="logo" to="/">2048</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView/>
  <footer>
    <p>© 2023 <a class="underline" href="https://twitter.com/Inno_Games">Inno Games Studio</a>. All rights reserved.</p>
  </footer>
</template>

<style>
.logo {
  font-size: 64px;
  color: #FFF;
  font-weight: bold;
  text-decoration: none;
}

footer {
  text-align: center;
  font-size: 12px;
  padding: 16px 0;
  color: #EEE;
}

footer a {
  color: #FFF;
}
</style>
