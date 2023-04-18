<template>
    <div>
      <side-bar></side-bar>
      <nav-bar></nav-bar>
      <Nuxt />
    </div>
</template>

<script>
import sideBar from '~/components/side-bar.vue'
import navBar from '~/components/nav-bar.vue'

export default{
  components: {
    sideBar,
    navBar
  }
}
</script>