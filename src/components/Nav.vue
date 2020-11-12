<template>
    <div class="nav">
        <div class="nav-item">
            <router-link to="/">Home</router-link>
        </div>
        <div class="nav-item">
            <router-link to="/LogIn">Log in</router-link>
        </div>
        <div class="nav-item">
            <router-link to="/About">About Us</router-link>
        </div>
        <div class="nav-item">
            <router-link to="/blog">Blog</router-link>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Nav"
    }
</script>

<style scoped lang="scss">
    .nav {
        display: flex;
        direction: rtl;
        text-align: right;
        flex-wrap: wrap;

        * {
            margin-left: 0.5rem;
            color: white !important;
            text-decoration: none !important;
        }

        a {
            padding: 0.5rem 1.5rem;
            display: inline-block;
            border-radius: 100px;
            transition: background-color 0.4s, color 0.4s;
            font-size: 1.2rem;

            &:hover {
                background: white !important;
                color: #752ba3 !important;

            }
        }
    }
</style>
