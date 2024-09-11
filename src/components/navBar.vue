<script setup>
import {computed, ref} from 'vue'
import menuIcon from '@heroicons/vue/20/solid/Bars3Icon'
import XMarkIcon from '@heroicons/vue/20/solid/XMarkIcon';
const emits = defineEmits(['showMenuEmit'])

const sideMenuShown = ref(false)
const showSideMenu = computed ({
  get() {
    return sideMenuShown.value
  },
  set(value) {
    sideMenuShown.value = value
  }
})
const currentHover = ref(null)
const activeHover = computed({
    get() {
        return currentHover.value
    },
    set(value) {
        currentHover.value = value
    }
})
function showMenu() {
    // emits("showMenuEmit")
    showSideMenu.value = !showSideMenu.value
}
 const navProps = defineProps({
    list: {
        type: Array,
        required: true
    }
 })
 const getRootList = computed(() => {
    return getNodeNameList(navProps.list)
 })
function closeSideMenu() {
    console.log('here')
  showSideMenu.value = false
}
</script>
<template>
    <div class="menu-overlay " :class="showSideMenu && 'show'">
        <div class="sidebar w-1/2 md:w-1/3" :class="showSideMenu && 'slide-right'">
            <div class="flex justify-between">
            <slot name="logo"></slot>
            <XMarkIcon @click="closeSideMenu" class="icon-medium-gray cursor-pointer" />
        </div>
        <div class="flex flex-col gap-4 w-1/3">
            <RouterLink v-for="item in navProps.list" :to="`/${item}`">
                {{ item }}
            </RouterLink>
        </div>
        </div>
    </div>
    <div class="flex w-full justify-between gap-x-4 top-banner">
        <slot name="logo"></slot>
        <menuIcon @click="showMenu" class="icon-medium-gray md:hidden cursor-pointer" />
        <nav class="hidden md:flex">
            <div class="flex items-center p-4 gap-x-10">
                <RouterLink class="nav-link" v-for="item in navProps.list" :to="`/${item}`">
                    {{ item }}
                </RouterLink>
            </div>
        </nav>
    </div>
</template>