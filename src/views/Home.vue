<template>
  <div class="home">
    <div class="background-container">
      <HomeBackground></HomeBackground>
    </div>
    <div class="top-bar">
      <div class="logo-container">
        <router-link to="/">
          <Logo></Logo>
        </router-link>
      </div>
      <div class="nav-container">
        <Nav></Nav>
      </div>
    </div>
    <div class="text-container">
      <Title></Title>
    </div>
    <div class="text-container">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Tincidunt vitae semper quis lectus nulla at volutpat diam. Consequat ac felis donec et odio. Arcu cursus euismod quis viverra nibh cras pulvinar mattis nunc.
      </p>
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
import Nav from '../components/Nav'
import Title from '../components/Title'

export default {
  name: 'Home',
  components: {
    // HelloWorld
    HomeBackground,
    Logo,
    Nav,
    Title
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
    margin: 4rem 4rem 0;
    padding: 0.5rem;
    vertical-align: middle;
  }

  .logo-container {
    width: 4rem;
    height: 4rem;
    display: inline-block;
    vertical-align: middle;
  }

  .nav-container {
    width: calc(100% - 4rem - 4rem);
    display: inline-block;
    vertical-align: middle;
  }

  .text-container {
    text-align: right;
    direction: rtl;

    p {
      width: 40%;
      margin-right: 10%;
      color: white;
      direction: ltr;
      text-align: justify;
      margin-top: 4rem;
      line-height: 150%;
      font-size: 1.2rem;
    }
  }
</style>
