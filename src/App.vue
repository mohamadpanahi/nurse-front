<template>
  <div id="app">
<!--    <div id="nav">-->
<!--      <router-link to="/">Home</router-link> |-->
<!--      <router-link to="/about">About</router-link>-->
<!--    </div>-->
    <router-view/>
  </div>
</template>

<style lang="scss">
    @font-face {
        font-family:"Vazir";
        src: url("assets/font/Vazir-FD.ttf");
        font-weight: 400;
    }

    @font-face {
        font-family:"Vazir";
        src: url("assets/font/Vazir-Bold-FD.ttf");
        font-weight: 700;
    }

    @font-face {
        font-family:"Vazir";
        src: url("assets/font/Vazir-Light-FD.ttf");
        font-weight: 100;
    }

    * {
        font-family: Vazir, sans-serif;
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        max-width: 1600px;
    }

    #nav {
        padding: 30px;

        a {
            font-weight: bold;
            color: #2c3e50;

            &.router-link-exact-active {
                color: #42b983;
            }
        }
    }
</style>
