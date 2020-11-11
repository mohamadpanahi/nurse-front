<template>
  <div class="home">
    <div class="background-container">
      <HomeBackground></HomeBackground>
    </div>
<!--    <img alt="Vue logo" src="../assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HomeBackground from '../components/HomeBackground'

export default {
  name: 'Home',
  components: {
    // HelloWorld
    HomeBackground
  }
}
</script>

<style scoped lang="scss">
  .home {
    width: 100vw;
    height: 100vh;
    vertical-align: middle;
    position: relative;
  }

  .background-container {
    text-align: left;
    width: 50vw;
    vertical-align: middle;
    transform: translateY(-50%);
    position: absolute;
    top: 50%;
    left: 0;
  }
</style>
