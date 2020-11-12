<template>
  <div class="home">
    <div class="background-container">
      <HomeBackground></HomeBackground>
    </div>
    <div class="top-bar">
      <div class="logo-container">
        <Logo></Logo>
      </div>
      <div class="nav-container">

      </div>
    </div>
<!--    <img alt="Vue logo" src="../assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HomeBackground from '../components/HomeBackground'
import Logo from '../components/Logo'

export default {
  name: 'Home',
  components: {
    // HelloWorld
    HomeBackground,
    Logo
  }
}
</script>

<style scoped lang="scss">
  .home {
    width: 100vw;
    height: 100vh;
    vertical-align: middle;
    position: relative;
    overflow: hidden;
    background-image: linear-gradient(to top right, rgba(69, 104, 220, 0.8), rgba(176, 106, 179, 0.8));
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

  .top-bar {
    margin: 4rem;
    padding: 0.5rem;
  }

  .logo-container {
    width: 4rem;
    height: 4rem;
  }
</style>
