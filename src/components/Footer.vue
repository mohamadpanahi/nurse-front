<template>
    <div class="footer">
        <div class="grid">
            <div class="info_links">
                <router-link to="/">
                    <div class="top">
                        <div class="logo-container">
                            <Logo></Logo>
                        </div>
                        <div class="name_logo">
                            مدکام
                        </div>
                    </div>
                </router-link>
                <div class="links">
                    <router-link to="/">صفحه اصلی</router-link>
                    <router-link to="/LogIn">ورود/ثبت نام</router-link>
                    <router-link to="/About">درباره ما</router-link>
                    <router-link to="/blog">وبلاگ</router-link>
                </div>
                <div class="copy_right">
                    تمام حقوق مادی و معنوی سایت متعلق به مدکام است. &copy;
                </div>
            </div>
            <div class="contacts">
                <div class="item">
                    <img class="contact-icon" src="../assets/logo.png" alt="Icon">
                    <div class="value">آدرس آدرس آدرس آدرس آدرس آدرس آدرس آدرس آدرس آدرس آدرس</div>
                </div>
                <div class="item">
                    <img class="contact-icon" src="../assets/logo.png" alt="Icon">
                    <div class="value">031-1234567</div>
                </div>
                <div class="item">
                    <img class="contact-icon" src="../assets/logo.png" alt="Icon">
                    <div class="value">jkdjskshjk@gmail.com</div>
                </div>
            </div>
            <div class="about_social">
                <p class="top">درباره مدکام</p>
                <p class="desc">
                    لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و سطرآنچنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز و کاربردهای متنوع با هدف بهبود ابزارهای کاربردی می باشد کتابهای زیادی در شصت و سه درصد گذشته حال و آینده
                </p>
                <div class="socials">
                    <img src="../assets/logo.png" alt="Icon" class="social-icon">
                    <img src="../assets/logo.png" alt="Icon" class="social-icon">
                    <img src="../assets/logo.png" alt="Icon" class="social-icon">
                    <img src="../assets/logo.png" alt="Icon" class="social-icon">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Logo from './Logo'

export default {
    name: 'Footer',
    components: {
        Logo
    }
}
</script>

<style scoped lang="scss">
    .footer {
        background-color: #555555;
        direction: rtl;
        padding-top: 6rem;
        padding-bottom: 4rem;
    }

    .grid {
        display: grid;
        grid-template-columns: 25% 25% 25%;
        justify-content: space-evenly;
    }

    .info_links {
        vertical-align: middle;
        text-align: right;
    }

    .logo-container {
        display: inline-block;
        max-width: 3rem;
        max-height: 3rem;
        vertical-align: middle;
        margin-left: 1rem;
        margin-right: 1rem;
    }

    .name_logo {
        display: inline-block;
        font-size: xx-large;
        font-weight: lighter;
        color: white !important;
        vertical-align: middle;
    }

    .links {
        margin-top: 2rem;
        margin-bottom: 2rem;

        & a {
            color: white !important;
            text-decoration: none !important;
            display: inline-block;
            padding-right: 1rem;
            border-left: 2px solid #AAAAAA;
            padding-left: 1rem;

            &:last-child {
                border: none;
            }
        }
    }

    .copy_right {
        color: white;
        font-size: small;
        font-weight: lighter;
        margin-right: 1rem;
    }

    .item {
        vertical-align: middle;
        margin-bottom: 2rem;
        text-align: right;
    }

    .contact-icon {
        display: inline-block;
        width: 3rem;
        height: 3rem;
        padding: 1rem;
        border-radius: 1000px;
        background-color: #333333;
        vertical-align: middle;
    }

    .value {
        width: calc(100% - 3rem - 1rem);
        text-align: justify;
        display: inline-block;
        padding-right: 1rem;
        color: white;
        vertical-align: middle;
    }

    .about_social {
        text-align: right;
    }

    .top {
        color: white;
        font-weight: bold;
    }

    .desc {
        color: #DDDDDD;
        font-weight: lighter;
        font-size: small;
        margin-top: 2rem;
        margin-bottom: 2rem;
        text-align: justify;
    }

    .socials {
        vertical-align: middle;
        text-align: center;
    }

    .social-icon {
        display: inline-block;
        width: 3rem;
        height: 3rem;
        padding: 1rem;
        border-radius: 0.25rem;
        background-color: #333333;
        vertical-align: middle;
        margin-left: 0.5rem;
    }
</style>