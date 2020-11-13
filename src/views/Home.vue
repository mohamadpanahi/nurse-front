<template>
  <div class="home">
    <div class="home-top">
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
          لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و سطرآنچنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز و کاربردهای متنوع با هدف بهبود ابزارهای کاربردی می باشد کتابهای زیادی در شصت و سه درصد گذشته حال و آینده شناخت فراوان جامعه و متخصصان را می طلبد
        </p>
      </div>
    </div>
    <div class="properties-container">
      <Properties></Properties>
    </div>
  </div>
</template>

<script>
import HomeBackground from '../components/HomeBackground'
import Logo from '../components/Logo'
import Nav from '../components/Nav'
import Title from '../components/Title'
import Properties from '../components/Properties'

export default {
  name: 'Home',
  components: {
    HomeBackground,
    Logo,
    Nav,
    Title,
    Properties
  }
}
</script>

<style scoped lang="scss">
  .home {
    padding: 0;
  }

  .home-top {
    width: 100%;
    height: 100vh;
    vertical-align: middle;
    position: relative;
    overflow: hidden;
    background-image: linear-gradient(to top right, rgba(69, 104, 220, 1), rgba(176, 106, 179, 1));
    margin-right: 0;
    margin-left: 0;
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
    margin: 3rem 4rem 0;
    padding: 0.5rem;
    vertical-align: middle;
  }

  .logo-container {
    width: 5rem;
    height: 5rem;
    display: inline-block;
    vertical-align: middle;

    padding: 1rem;
    overflow: visible;
    background: rgba(255, 255, 255, 0.0);
    border-radius: 100px;
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
      margin-right: 8rem;
      color: white;
      direction: rtl;
      text-align: justify;
      margin-top: 6rem;
      line-height: 200%;
      font-size: 1.2rem;
    }
  }
</style>
