<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <h1 class="hehe"></h1>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
<style scoped>
  .hehe {color: black}  
<style>

