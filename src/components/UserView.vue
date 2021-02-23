<template>
    <div class="card" v-if="user.login">
        <img :src="user.avatar_url" width="128" style="float: right;border-radius: 25%;margin: 20px 10px;">
        <h2 style="margin-bottom: 0;">{{user.name}}</h2>
        <a href="https://github.com/dzshn" target="_blank" rel="noopener noreferrer">
            <small>dzshn @ <i class="bi-github"></i></small>
        </a>
        <p>{{user.bio}}</p>
        <small>
            <i class="bi-people"></i> {{user.followers}} follower{{user.followers == 1? '' : 's'}} · {{user.following}} following <br>
            <i class="bi-box"></i> {{user.public_repos}} repos · {{user.public_gists}} gists <br>
            <i class="bi-building"></i> {{user.company}} ·
            <i class="bi-geo-alt"></i> {{user.location}} ·
            <i class="bi-envelope"></i> {{user.email}}zshn@pm.me ·
            <a
                :href="user.blog"
                target="_blank" rel="noopener noreferrer"
            >
                <i class="bi-file-earmark-text"></i>
                {{user.blog.replace('https://', '')}}
            </a> ·
            <a
                :href="'https://twitter.com/@'+user.twitter_username"
                target="_blank" rel="noopener noreferrer"
            >
                <i class="bi-twitter"></i> {{user.twitter_username}}
            </a>
        </small>
    </div>
    <div v-else-if="error" class="card">
        <h1>Error loading user :/</h1>
        <p>{{error}}</p>
    </div>
    <h1 v-else class="card">loading user...</h1>
</template>

<script>
export default {
    data() {
        return {
            user: {},
            error: null
        }
    },
    mounted() {
        fetch('https://api.github.com/users/dzshn').then(
            response => {
                if (response.ok) {
                    response.json().then(json => {this.user = json})
                }
                else {this.error = `HTTP Error: ${response.status} ${response.statusText}!`}
            }
        ).catch(
            error => {this.error = error}
        )
    }
}
</script>