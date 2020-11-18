<template>
    <div class="login-parent">
        <p class="subject">
            فرصت را از دست ندهید ...
        </p>
        <div class="login_cards">
            <div class="card nurse">
                <div class="top">
                    <p class="title">پرستار</p>
                    <img src="../assets/nurse.png" alt="Nurse">
                </div>
                <div class="desc">
                    لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و سطرآنچنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز و کاربردهای متنوع با هدف بهبود ابزارهای کاربردی می باشد کتابهای زیادی در شصت و سه درصد گذشته حال و آینده
                </div>
                <div class="button nurse-button">
                    ثبت نام
                </div>
            </div>
            <div class="card user">
                <div class="top">
                    <p class="title">کاربر</p>
                    <img src="../assets/user.png" alt="User">
                </div>
                <div class="desc">
                    لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و سطرآنچنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز و کاربردهای متنوع با هدف بهبود ابزارهای کاربردی می باشد کتابهای زیادی در شصت و سه درصد گذشته حال و آینده
                </div>
                <div class="button user-button">
                    ثبت نام
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "LoginCards"
    }
</script>

<style scoped lang="scss">
    .login-parent {
        padding-top: 6rem;
    }

    .login_cards {
        display: grid;
        grid-template-columns: 25% 25%;
        justify-content: space-evenly;
        padding-bottom: 4rem;
        padding-top: 6rem;
    }

    .subject {
        direction: rtl;
        font-size: xx-large;
        font-weight: bolder;
    }

    .card {
        box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.8);
        padding: 2rem;
        direction: rtl;
        color: #EEEEEE;
        border-radius: 0.5rem;
    }

    .nurse {
        background-image: linear-gradient(to top, rgba(33, 55, 127, 0.9), rgba(33, 55, 127, 0.9)), linear-gradient(to top right, #000, #000);
    }

    .user {
        background-image: linear-gradient(to top, rgba(115, 51, 118, 0.9), rgba(115, 51, 118, 0.9)), linear-gradient(to top right, #000, #000);
    }

    .title {
        display: inline-block;
        vertical-align: middle;
    }

    img {
        max-width: 4rem;
        max-height: 4rem;
        display: inline-block;
        vertical-align: middle;
        transform: translateX(50%);
    }

    .top {
        font-size: xx-large;
        font-weight: lighter;
        direction: ltr;
        vertical-align: middle;
        margin-bottom: 2rem;
        text-align: center;
    }

    .desc {
        text-align: justify;
        font-weight: lighter;
        margin-right: 15%;
        margin-left: 15%;
        margin-bottom: 2rem;
    }

    .button {
        border-radius: 1000px;
        background: white;
        margin: auto;
        display: inline-block;
        padding: 0.5rem 2rem;
        font-weight: bolder;
        font-size: large;
        cursor: pointer;
    }

    .nurse-button {
        color: rgba(115, 51, 118, 1);
        transition: color 0.4s, background-color 0.4s;

        &:hover {
            color: white;
            background: rgba(115, 51, 118, 1);
        }
    }

    .user-button {
        color: rgba(33, 55, 127, 1);
        transition: color 0.4s, background-color 0.4s;

        &:hover {
            color: white;
            background: rgba(33, 55, 127, 1);
        }
    }
</style>
