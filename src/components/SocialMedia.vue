<template>
    <div class="card">
        <h2>contact and social media stuff:</h2>
        <div>
            <div v-for="(link, index) in mediaLinks" :key="'l-'+index">
                <a :href="'https://'+link.url" target="_blank" rel="noopener noreferrer">
                    <i :class="'bi-'+link.icon" v-if="link.icon"></i>
                    <i v-else class="bi-link-45deg"></i>
                    {{link.user}} <small>@{{link.at}}</small>
                </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            mediaLinks: require('../assets/mediaLinks').default
        }
    }
}
</script>

<style scoped lang="stylus">
.card > div
    display flex
    flex-wrap wrap
    justify-content center
    text-align center
    margin 5px 40px
    max-width 580px
    div
        background linear-gradient(to right, #353535, #444)
        border-radius 5px
        min-width fit-content
        margin 5px
        padding 3px 8px 5px
        transition-duration 140ms
        transition-timing-function cubic-bezier(0.175, 0.885, 0.32, 1.275)
        &:hover
            scale 1.06

small
    color #eee
</style>