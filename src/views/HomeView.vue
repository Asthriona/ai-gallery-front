<template>
  <div class="home">
    <gallery msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import gallery from '@/components/gallery.vue'

export default {
  name: 'HomeView',
  components: {
    gallery
  }
}
</script>
