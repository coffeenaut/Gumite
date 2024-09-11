<script setup>
import { RouterView } from 'vue-router'
import NavBar from './components/navBar.vue'

const links = ["home", "info", "blogs"]
</script>
<template>
    <div class="flex flex-col w-full">
      <div class="flex w-full">
        <NavBar :list="links">
          <template #logo>
            <img src="./assets/Gx250.svg" />
          </template>
        </NavBar>
      </div>
      <div class="flex w-full">
        <RouterView />
      </div>
    </div>
</template>
