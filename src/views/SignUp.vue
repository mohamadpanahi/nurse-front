<template>
    <div class="sign-up">
        <div class="container">
            <p class="title">
                ثبت نام
            </p>
            <form>
                <div class="grid">
                    <div class="item">
                        <label for="name">نام</label>
                        <input type="text" id="name" name="name" placeholder="نام خود را وارد کنید" required
                               v-model="user_name">
                    </div>
                    <div class="item">
                        <label for="phone">تلفن همراه</label>
                        <input type="tel" id="phone" name="phone" placeholder="0 9 - - - - - - - -" minlength="11"
                               maxlength="11" required v-model="user_phone" @blur="check_phone">
                    </div>
                    <div class="item">
                        <label for="password">رمز عبور</label>
                        <input type="password" id="password" name="password" placeholder="**********" required
                               v-model="user_password">
                    </div>
                    <div class="item">
                        <label for="confirm-password">تکرار رمز عبور</label>
                        <input type="password" id="confirm-password" name="confirm-password" placeholder="**********"
                               required v-model="user_confirm">
                    </div>
                    <div class="item">
                        <label for="email">پست الکترونیک</label>
                        <input type="email" id="email" name="email" placeholder="abcdefg@hijkl.mno"
                               v-model="user_email">
                    </div>
                    <div class="item">
                        <label for="province">استان</label>
                        <input type="text" id="province" name="province" placeholder="تهران" required
                               v-model="user_province">
                    </div>
                    <div class="item">
                        <label for="city">شهر</label>
                        <input type="text" id="city" name="city" placeholder="تهران" required v-model="user_city">
                    </div>
                    <div class="item">
                        <label for="add">آدرس</label>
                        <input type="text" id="add" name="add" placeholder="خیابان ..." required v-model="user_add">
                    </div>
                    <div class="item map-root">
                        <label class="map-title">آدرس روی نقشه</label>
                        <div class="map-container">
                            <div id="map"></div>
                            <img src="../assets/pin.svg" id="pin" alt="location">
                        </div>
                    </div>
                    <div class="item" id="role-container">
                        <p class="role-title">نقش</p>
                        <label for="role-nurse">پرستار</label>
                        <input type="radio" id="role-nurse" name="role" value="nurse" required v-model="user_role">
                        <label for="role-user">کاربر</label>
                        <input type="radio" id="role-user" name="role" value="user" required checked
                               v-model="user_role">
                    </div>
                </div>
                <div class="button">
                    <div class="button-container">
                        <input v-show="!phone_checked || !not_empty" type="submit" value="ثبت نام" id="submit0" @click="do_signup" disabled>
                        <input v-show="phone_checked && not_empty" type="submit" value="ثبت نام" id="submit" @click="do_signup">
                    </div>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    import Map from 'ol/Map';
    import View from 'ol/View';
    import TileLayer from 'ol/layer/Tile';
    import XYZ from 'ol/source/XYZ';
    import Overlay from 'ol/Overlay';
    import {fromLonLat, toLonLat} from 'ol/proj';

    import VectorLayer from 'ol/layer/Vector';
    import VectorSource from 'ol/source/Vector';
    import Control from 'ol/control/Control';
    import Feature from 'ol/Feature';
    import Point from 'ol/geom/Point';
    import {Circle, Circle as CircleStyle, Fill, Stroke, Style} from 'ol/style';

    import Geolocation from 'ol/Geolocation';

    import axios from 'axios'

    export default {
        name: 'Home',
        data() {
            return {
                user_name: '',
                user_phone: '',
                user_password: '',
                user_confirm: '',
                user_email: '',
                user_role: 'user',
                user_province: '',
                user_city: '',
                user_add: '',
                user_location: {},
                user_address: {
                    province: '',
                    city: '',
                    add: '',
                    location: ''
                },
                phone_checked: false
            }
        },
        watch: {
            user_province(to) {
                this.user_address.province = to
            },
            user_city(to) {
                this.user_address.city = to
            },
            user_add(to) {
                this.user_address.add = to
            },
            user_location(to) {
                this.user_address.location = to
            }
        },
        computed: {
            not_empty() {
                return !!(this.user_name && this.user_phone && this.user_password && this.user_role && this.user_province && this.user_city &&
                    this.user_add && this.user_location && this.user_location.location && this.user_location.location[0]
                    && this.user_location.location[1])
            },
            signup_request() {
                if (this.email)
                    return {
                        name: this.user_name,
                        phone: this.user_phone,
                        password: this.user_password,
                        email: this.user_email,
                        role: this.user_role,
                        address: this.user_address
                    }
                else
                    return {
                        name: this.user_name,
                        phone: this.user_phone,
                        password: this.user_password,
                        role: this.user_role,
                        address: this.user_address
                    }
            }
        },
        components: {},
        methods: {
            do_signup(e) {
                e.preventDefault()
                axios({
                    method: 'POST',
                    url: 'localhost:8080/api/v1/signup',
                    data: this.signup_request
                })
                    .then(function (response) {
                        console.log(response);
                    })
                    .catch(function (error) {
                        console.log(error);
                    })
            },
            check_phone() {
                axios({
                    method: 'GET',
                    url: 'localhost:8080/isFree',
                    data: {
                        phone: this.user_phone
                    }
                })
                    .then(function (response) {
                        this.phone_checked = true
                    })
                    .catch(function (error) {
                        this.phone_checked = false
                    })
            }
        },
        mounted() {
            // for pin
            const overlay = new Overlay({
                element: document.getElementById('pin'),
                autoPan: true,
                autoPanAnimation: {
                    duration: 250
                }
            });

// map
            const view = new View({
                center: fromLonLat([51.678, 32.658]),
                zoom: 12,
                enableRotation: false
            });

            const map = new Map({
                target: 'map',
                layers: [
                    new TileLayer({
                        source: new XYZ({
                            url: 'http://mt{0-3}.google.com/vt/lyrs=m&hl=fa&x={x}&y={y}&z={z}'
                            // url:
                            //   'https://developers.parsijoo.ir/web-service/v1/map/?type=tile&x={x}&y={y}&z={z}&apikey=d1867d1ead0148eaaf7f40d4a679c50f'
                        })
                    })
                ],
                overlays: [overlay],
                view
            });

// handle click and move pin
            map.on('singleclick', e => {
                this.user_location = {
                    location: toLonLat(e.coordinate)
                }
                overlay.setPosition(e.coordinate);
            });

// gps
            const geolocation = new Geolocation({
                // enableHighAccuracy must be set to true to have the heading value.
                trackingOptions: {
                    enableHighAccuracy: true
                },
                projection: view.getProjection()
            });

            geolocation.setTracking(true);

            const accuracyFeature = new Feature();
            const positionFeature = new Feature();

            positionFeature.setStyle(
                new Style({
                    image: new CircleStyle({
                        radius: 6,
                        fill: new Fill({
                            color: '#3399CC'
                        }),
                        stroke: new Stroke({
                            color: '#fff',
                            width: 2
                        })
                    })
                })
            );

            geolocation.on('change:accuracyGeometry', function () {
                accuracyFeature.setGeometry(geolocation.getAccuracyGeometry());
            });

            geolocation.on('change:position', function () {
                const coordinates = geolocation.getPosition();
                positionFeature.setGeometry(coordinates ? new Point(coordinates) : null);
            });

            const source = new VectorSource({
                features: [accuracyFeature, positionFeature]
            });

            new VectorLayer({map, source});

// add GPS button
            const locate = document.createElement('div');
            locate.className = 'ol-control ol-unselectable locate';
            locate.innerHTML = `<button title="Locate me"><svg xmlns="http://www.w3.org/2000/svg" xmlns:svgjs="http://svgjs.com/svgjs" version="1.1" x="0" y="0" viewBox="0 0 469.333 469.333" style="display: block" xml:space="preserve" class=""><g transform="matrix(0.68,0,0,0.68,75.09343750000002,75.09343750000008)">
<path xmlns="http://www.w3.org/2000/svg" d="M234.667,149.333c-47.147,0-85.333,38.187-85.333,85.333S187.52,320,234.667,320S320,281.813,320,234.667  S281.813,149.333,234.667,149.333z M425.387,213.333C415.573,124.373,344.96,53.76,256,43.947V0h-42.667v43.947  C124.373,53.76,53.76,124.373,43.947,213.333H0V256h43.947c9.813,88.96,80.427,159.573,169.387,169.387v43.947H256v-43.947  C344.96,415.573,415.573,344.96,425.387,256h43.947v-42.667H425.387L425.387,213.333z M234.667,384  c-82.453,0-149.333-66.88-149.333-149.333s66.88-149.333,149.333-149.333S384,152.213,384,234.667S317.12,384,234.667,384z" fill="#666666" data-original="#000000"/>
</svg></button>`;

            locate.addEventListener('click', function () {
                if (!source.isEmpty()) {
                    map.getView().fit(source.getExtent(), {
                        maxZoom: 16,
                        duration: 500
                    });
                }
            });

            map.addControl(
                new Control({
                    element: locate
                })
            );

// set initial location
            window.addEventListener('load', () => {
                setTimeout(() => {
                    if (!source.isEmpty()) {
                        map.getView().fit(source.getExtent(), {
                            maxZoom: 16,
                            duration: 500
                        });
                    }
                }, 500);
            });
        }
        /*
        POST /api/v1/signup
        {
          ,'علی سالمی' :*name
          phone*: '09123456789',
          password*: '12345678',
          email,
          role*: 'user || nurse',
          address*: {
            ,'اصفهان' :*province
            ,'خمینی شهر' :*city
            ,'خیابان ...' :*add
            location*: {
              coordinates*: [12.25, -23.63]
            }
          }
        }
        */
    }
</script>

<style scoped lang="scss">
    .map-title {
        margin-bottom: 1rem;
    }

    .map-root {
        position: relative;
        grid-column: 2 span;
        margin-bottom: 1rem;
    }

    .map-container {
        top: 0;
        left: 0;
        width: 100%;
        height: 30rem;
        /*outline: rgba(0, 0, 255, 1) wave 4px;*/
        outline: 4px solid rgba(0, 0, 255, 0.8);
        direction: ltr;
    }

    #map {
        width: 100%;
        height: 100%;
    }

    #pin {
        display: block;
        position: absolute;
        width: 2rem;
        transform: translate(-50%, -100%);
    }

    .sign-up {
        background-image: linear-gradient(30deg, #d704a2, #490871);
        width: 100%;
        min-height: 100vh;
        padding-top: 6rem;
        padding-bottom: 4rem;
        text-align: center;
        direction: rtl;
    }

    .container {
        width: 50%;
        margin: auto;
        background-color: white;
        border-radius: 1rem;
        box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
        padding: 2rem;
    }

    .title {
        font-size: xx-large;
        font-weight: bolder;
        text-align: right;
        margin-bottom: 2rem;
    }

    .grid {
        display: grid;
        grid-template-columns: 45% 45%;
        justify-content: space-between;
    }

    input, label {
        display: block;
    }

    input {
        direction: rtl;
        width: 100%;
        margin-bottom: 1rem;
        padding: 0.5rem 1rem;
        background-color: #EEEEEE;
        border: 1px solid #AAAAAA !important;
        border-radius: 0.25rem !important;
    }

    label {
        text-align: right;
        margin-bottom: 0.25rem;
    }

    #phone, #email, #password, #confirm-password {
        direction: ltr;
    }

    #role-container {
        text-align: right;
        grid-column: 2 span;

        * {
            display: inline-block;
            text-align: right;
        }

        input {
            width: auto;
            margin-left: 2rem;
        }

        label {
            padding-left: 1rem;
        }

        p {
            display: block;
            margin-bottom: 0.25rem;
            font-size: large;
        }
    }

    .button {
        text-align: right;

        .button-container {
            display: inline-block;
        }

        #submit, #submit0 {
            font-size: large;
            font-weight: bold;
            color: white;
            background-color: #2a4ebd;
            display: inline-block;
            padding: 0.5rem 3rem;
            border-radius: 0.25rem;
            cursor: pointer;
            margin: 2rem auto 0;
        }
    }

    /* map css */
    .ol-box {
        box-sizing: border-box;
        border-radius: 2px;
        border: 2px solid #00f;
    }

    .ol-mouse-position {
        top: 8px;
        right: 8px;
        position: absolute;
    }

    .ol-scale-line {
        background: rgba(0, 60, 136, 0.3);
        border-radius: 4px;
        bottom: 8px;
        left: 8px;
        padding: 2px;
        position: absolute;
    }

    .ol-scale-line-inner {
        border: 1px solid #eee;
        border-top: none;
        color: #eee;
        font-size: 10px;
        text-align: center;
        margin: 1px;
        will-change: contents, width;
        transition: all 0.25s;
    }

    .ol-scale-bar {
        position: absolute;
        bottom: 8px;
        left: 8px;
    }

    .ol-scale-step-marker {
        width: 1px;
        height: 15px;
        background-color: #000;
        float: right;
        z-index: 10;
    }

    .ol-scale-step-text {
        position: absolute;
        bottom: -5px;
        font-size: 12px;
        z-index: 11;
        color: #000;
        text-shadow: -2px 0 #fff, 0 2px #fff, 2px 0 #fff, 0 -2px #fff;
    }

    .ol-scale-text {
        position: absolute;
        font-size: 14px;
        text-align: center;
        bottom: 25px;
        color: #000;
        text-shadow: -2px 0 #fff, 0 2px #fff, 2px 0 #fff, 0 -2px #fff;
    }

    .ol-scale-singlebar {
        position: relative;
        height: 10px;
        z-index: 9;
        box-sizing: border-box;
        border: 1px solid #000;
    }

    .ol-unsupported {
        display: none;
    }

    .ol-unselectable,
    .ol-viewport {
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        -webkit-tap-highlight-color: transparent;
    }

    .ol-selectable {
        -webkit-touch-callout: default;
        -webkit-user-select: text;
        -moz-user-select: text;
        -ms-user-select: text;
        user-select: text;
    }

    .ol-grabbing {
        cursor: -webkit-grabbing;
        cursor: -moz-grabbing;
        cursor: grabbing;
    }

    .ol-grab {
        cursor: move;
        cursor: -webkit-grab;
        cursor: -moz-grab;
        cursor: grab;
    }

    .ol-control {
        position: absolute;
        background-color: rgba(255, 255, 255, 0.4);
        border-radius: 4px;
        padding: 2px;
    }

    .ol-control:hover {
        background-color: rgba(255, 255, 255, 0.6);
    }

    .ol-zoom {
        top: 0.5em;
        left: 0.5em;
    }

    .ol-rotate {
        top: 0.5em;
        right: 0.5em;
        transition: opacity 0.25s linear, visibility 0s linear;
    }

    .ol-rotate.ol-hidden {
        opacity: 0;
        visibility: hidden;
        transition: opacity 0.25s linear, visibility 0s linear 0.25s;
    }

    .ol-zoom-extent {
        top: 4.643em;
        left: 0.5em;
    }

    .ol-full-screen {
        right: 0.5em;
        top: 0.5em;
    }

    .ol-control button {
        display: block;
        margin: 1px;
        padding: 0;
        color: #fff;
        font-size: 1.14em;
        font-weight: 700;
        text-decoration: none;
        text-align: center;
        height: 1.375em;
        width: 1.375em;
        line-height: 0.4em;
        background-color: rgba(0, 60, 136, 0.5);
        border: none;
        border-radius: 2px;
    }

    .ol-control button::-moz-focus-inner {
        border: none;
        padding: 0;
    }

    .ol-zoom-extent button {
        line-height: 1.4em;
    }

    .ol-compass {
        display: block;
        font-weight: 400;
        font-size: 1.2em;
        will-change: transform;
    }

    .ol-touch .ol-control button {
        font-size: 1.5em;
    }

    .ol-touch .ol-zoom-extent {
        top: 5.5em;
    }

    .ol-control button:focus,
    .ol-control button:hover {
        text-decoration: none;
        background-color: rgba(0, 60, 136, 0.7);
    }

    .ol-zoom .ol-zoom-in {
        border-radius: 2px 2px 0 0;
    }

    .ol-zoom .ol-zoom-out {
        border-radius: 0 0 2px 2px;
    }

    .ol-attribution {
        text-align: right;
        bottom: 0.5em;
        right: 0.5em;
        max-width: calc(100% - 1.3em);
    }

    .ol-attribution ul {
        margin: 0;
        padding: 0 0.5em;
        color: #000;
        text-shadow: 0 0 2px #fff;
    }

    .ol-attribution li {
        display: inline;
        list-style: none;
    }

    .ol-attribution li:not(:last-child):after {
        content: ' ';
    }

    .ol-attribution img {
        max-height: 2em;
        max-width: inherit;
        vertical-align: middle;
    }

    .ol-attribution button,
    .ol-attribution ul {
        display: inline-block;
    }

    .ol-attribution.ol-collapsed ul {
        display: none;
    }

    .ol-attribution:not(.ol-collapsed) {
        background: rgba(255, 255, 255, 0.8);
    }

    .ol-attribution.ol-uncollapsible {
        bottom: 0;
        right: 0;
        border-radius: 4px 0 0;
    }

    .ol-attribution.ol-uncollapsible img {
        margin-top: -0.2em;
        max-height: 1.6em;
    }

    .ol-attribution.ol-uncollapsible button {
        display: none;
    }

    .ol-zoomslider {
        top: 4.5em;
        left: 0.5em;
        height: 200px;
    }

    .ol-zoomslider button {
        position: relative;
        height: 10px;
    }

    .ol-touch .ol-zoomslider {
        top: 5.5em;
    }

    .ol-overviewmap {
        left: 0.5em;
        bottom: 0.5em;
    }

    .ol-overviewmap.ol-uncollapsible {
        bottom: 0;
        left: 0;
        border-radius: 0 4px 0 0;
    }

    .ol-overviewmap .ol-overviewmap-map,
    .ol-overviewmap button {
        display: inline-block;
    }

    .ol-overviewmap .ol-overviewmap-map {
        border: 1px solid #7b98bc;
        height: 150px;
        margin: 2px;
        width: 150px;
    }

    .ol-overviewmap:not(.ol-collapsed) button {
        bottom: 1px;
        left: 2px;
        position: absolute;
    }

    .ol-overviewmap.ol-collapsed .ol-overviewmap-map,
    .ol-overviewmap.ol-uncollapsible button {
        display: none;
    }

    .ol-overviewmap:not(.ol-collapsed) {
        background: rgba(255, 255, 255, 0.8);
    }

    .ol-overviewmap-box {
        border: 2px dotted rgba(0, 60, 136, 0.7);
    }

    .ol-overviewmap .ol-overviewmap-box:hover {
        cursor: move;
    }

    /*others styles*/
    .ol-control {
        position: absolute;
        padding: 2px;
        transition: all 0.2s ease;
    }

    .ol-control button {
        display: block;
        margin: 8px 0;
        padding: 0.3rem;
        height: 2rem;
        width: 2rem;

        color: #666;
        background-color: #ffffff;

        font-size: 1.14rem;
        font-weight: 700;
        text-decoration: none;
        text-align: center;
        line-height: 0.4em;

        border: none;
        border-radius: 5px;
        box-shadow: 0 2px 8px 1px rgba(0, 0, 0, 0.3);
        transition: all 0.2s ease;
    }

    .ol-control button::-moz-focus-inner {
        border: none;
        padding: 0;
    }

    .ol-control button:focus {
        outline: none;
        text-decoration: none;
        box-shadow: 0 2px 8px 1px rgba(0, 0, 0, 0.3);
    }

    .ol-control button:hover {
        text-decoration: none;
        box-shadow: 0 2px 10px 1px rgba(0, 0, 0, 0.5);
        outline: none;
    }

    .locate {
        bottom: calc(4.5rem + 16px);
        left: .5rem;
    }

    .ol-zoom {
        bottom: 0.5rem;
        left: 0.5rem;
    }
</style>
