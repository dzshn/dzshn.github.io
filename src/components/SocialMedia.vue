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

<style scoped>
.card > div {
    display: flex;
    text-align: center;
    flex-wrap: wrap;
    margin: 5px 40px;
    max-width: 580px;
    justify-content: center;
}

.card > div > div {
    min-width: fit-content;
    margin: 5px;
    background: linear-gradient(to right, #353535, #444);
    padding: 3px 8px 5px;
    border-radius: 5px;
    transition-duration: 140ms;
    transition-timing-function: cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.card > div > div:hover {
    scale: 1.06;
}

small {
    color: #eee;
}
</style>