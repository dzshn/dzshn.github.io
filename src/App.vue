<template>
    <div class="card">
        <h1>hi! I'm z, I do code stuff</h1>
        <p>
            ..and this is my website, nothing special about it, mostly something for me to play
            around with and have some sort of introduction to share :P <br> <br>

            there may be some broken layout on your end, but that's just because I'm too lazy for
            testing other browsers, send me a screenshot and I'll try to fix it, erh, if you want to,
            of course.. <br> <br>

            also check out the subdomain I put my stuff on right
            <a href="https://stuff.dzshn.xyz" target="_blank" rel="noopener noreferrer">here</a>
        </p>
    </div>

    <div class="card">
        <h2>little bit about me:</h2>
        <p>
            I'm an 1× year old dev, not much experienced, I mostly use vue.js for some webapps, and
            python for automation stuff and bots <br> <br>

            I'm MtF trans, I go by she/her and Sofia (or Chloe, still not entirely sure about names yet),
            but online people call me by z or zsh (yep,
            <a href="https://en.wikipedia.org/wiki/Z_shell" target="_blank" rel="noopener noreferrer">that command shell</a>)
            <br> <br>

            I used to do some weird animations in blender, poorly, <del>they're in my youtube which is
            linked below if you want to check it out</del> well, not anymore since I got my Google
            account deleted.. I may repost them some day
        </p>
    </div>

    <SocialMedia/>

    <h2 class="card">well, here's some stuff from my github profile:</h2>
    <UserView/>

    <h2 class="card">...some recent activity:</h2>
    <ActivityView/>

    <h2 class="card">..my repos:</h2>
    <RepoView/>

    <h2 class="card">..and that's it for now!</h2>

    <footer>
        MIT License Copyright © 2021 dzshn ·
        <a href="https://github.com/dzshn/webpage" target="_blank" rel="noopener noreferrer">
            view source <i class="bi-code-square"></i>
        </a>
        · made with
        <a href="https://vuejs.org" target="_blank" rel="noreferrer noopener">
            vue.js <i class="bi-link-45deg"></i>
        </a>
        · deployed with
        <a href="https://www.netlify.com/" target="_blank" rel="noreferrer noopener">
            netlify <i class="bi-link-45deg"></i>
        </a>
    </footer>
</template>

<script>
import RepoView from "./components/RepoView"
import UserView from "./components/UserView"
import ActivityView from "./components/ActivityView"
import SocialMedia from "./components/SocialMedia"

export default {
    name: 'App',
    components: {
        RepoView,
        UserView,
        ActivityView,
        SocialMedia
    }
}
</script>

<style lang="stylus">
@import "https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css"

body
    background linear-gradient(to right, #fed3ea, #e0c2e3)
    font-family Avenir, Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #eee
    margin 40px 0 0

a
    text-decoration none
    color #eee
    footer &
    .card &
        color #fff
        font-weight 600

footer
    background linear-gradient(to right, #222, #1a1a1a)
    margin-top 50px
    padding 10px 0
    width 100%

.card
    font-size large
    background linear-gradient(to right, #222, #1a1a1a)
    padding 2px 15px 8px
    margin 10px auto
    border-radius 8px
    width fit-content
    max-width 90%
    text-align start
    h2&
        padding 8px
        &:nth-of-type(1)
            margin-left 10%
            margin-right 5%

        &:nth-of-type(2)
            margin-left 15%

        &:nth-of-type(3)
            margin-right 15%

        &:nth-of-type(4)
            @media screen and (max-width 600px)
                margin-right 6%
</style>