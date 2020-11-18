<template>
    <div class="nav">
        <div class="nav-item">
            <router-link to="/">صفحه اصلی</router-link>
        </div>
        <div class="nav-item">
            <router-link to="/LogIn">ورود/ثبت نام</router-link>
        </div>
        <div class="nav-item">
            <router-link to="/About">درباره ما</router-link>
        </div>
        <div class="nav-item" @click="clicked">
            <router-link to="/blog">وبلاگ</router-link>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Nav",
        methods:{
            click() {
                //send request
            }
        }
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
