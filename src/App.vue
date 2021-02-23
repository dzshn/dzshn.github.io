<template>
    <div class="card">
        <h1>hi! I'm z, I do code stuff</h1>
        <p>
            ..and this is my website, nothing special about it, mostly something for me to play
            around with and have some sort of introduction to share :P <br> <br>

            there may be some broken layout on your end, but that's just because I'm too lazy for
            testing other browsers, send me a screenshot and I'll try to fix it, erh, if you want to,
            of course.. <br> <br>
        </p>
    </div>

    <div class="card">
        <h3>little bit about me:</h3>
        <p>
            I'm an 1× year old dev, not much experienced, I mostly use vue.js for some webapps, and
            python for automation stuff and bots <br> <br>

            I'm MtF trans, I go by she/her and Sofia or Chloe (not entirely sure about names yet),
            but online people call me by z or zsh (yep,
            <a href="https://en.wikipedia.org/wiki/Z_shell" target="_blank" rel="noopener noreferrer">that command shell</a>)
            <br> <br>

            I used to do some weird animations in blender, poorly, they're in my youtube which is
            linked below if you want to check it out
        </p>
    </div>

    <div class="card">
        <h2>contact and social media stuff:</h2>
        <p style="margin: 5px 40px; text-align: center; line-spacing: 10px;">
            <span v-for="(link, index) in mediaLinks" :key="'l-'+index">
                {{index % 3? '·' : ''}}
                <a :href="'https://'+link.url" target="_blank" rel="noopener noreferrer">
                    <i :class="'bi-'+link.icon" v-if="link.icon"></i>
                    {{link.user}} <small style="color: #eee;">@{{link.at}}</small>
                </a> <br v-if="(index + 1) % 3 == 0">
            </span>
        </p>
    </div>

    <h2 class="card">well, here's some stuff from my github profile:</h2>
    <UserView/>

    <h2 class="card">...some recent activity:</h2>
    <ActivityView/>

    <h2 class="card">..my repos:</h2>
    <RepoView/>

    <h2 class="card">..and that's it for now!</h2>

    <footer>
        MIT License Copyright © 2021 dzshn ·
        <a href="https://github.com/dzshn/dzshn.github.io" target="_blank" rel="noopener noreferrer">
            view source <i class="bi-code-square"></i>
        </a>
        · made with
        <a href="https://vuejs.org" target="_blank" rel="noreferrer noopener">
            vue.js <i class="bi-link-45deg"></i>
        </a>
    </footer>
</template>

<script>
import RepoView from "./components/RepoView.vue"
import UserView from "./components/UserView.vue"
import ActivityView from "./components/ActivityView.vue"
import { mediaLinks } from "./assets/mediaLinks"

export default {
    name: 'App',
    components: {
        RepoView,
        UserView,
        ActivityView
    },
    data() {
        return {
            mediaLinks: mediaLinks
        }
    }
}
</script>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css");

body {
    background: linear-gradient(to right, #fed3ea, #e0c2e3);
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #eee;
    margin: 40px 0 0;
}

a {
    text-decoration: none;
    color: #fff;
}

footer {
    color: #eee;
    position: relative;
    bottom: 0;
    width: 100%;
    background: linear-gradient(to right, #222, #1a1a1a);
    padding: 10px 0px;
    margin-top: 50px;
}

footer a, .card a {
    font-weight: 600;
}

.card {
    font-size: large;
    background: linear-gradient(to right, #222, #1a1a1a);
    padding: 2px 15px 8px;
    margin: 10px auto;
    border-radius: 8px;
    width: fit-content;
    max-width: 90%;
    text-align: start;
}

h2.card{
    padding: 8px;
}

h2.card:nth-of-type(1) {
    margin-left: 10%;
    margin-right: 5%;
}

h2.card:nth-of-type(2) {
    margin-left: 15%;
}

h2.card:nth-of-type(3) {
    margin-right: 15%;
}

@media screen and (max-width: 600px) {
    h2.card:nth-of-type(4) {
        margin-right: 6%;
    }
}
</style>