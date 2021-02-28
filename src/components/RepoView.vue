<template>
    <div id="componentRoot" v-if="repos.length > 0">
        <a v-for="repo in repos" :key="'repo-'+repo.id" :href="repo.html_url" target="_blank" rel="noopener noreferrer">
            <div class="card">
                <h2><small>dzshn/</small> {{repo.name}}</h2>
                <p>{{repo.description}}</p>
                <small>
                    {{repo.language ?? 'No lang'}} /
                    <a
                        v-if="repo.license"
                        :href="'https://choosealicense.com/licenses/'+repo.license.key+'/'"
                        target="_blank" rel="noopener noreferrer"
                    >
                        {{repo.license.name}}
                        <i class="bi-link-45deg"></i>
                    </a>
                    <span v-else>No license</span>
                    <a v-if="repo.homepage" :href="repo.homepage" target="_blank" rel="noopener noreferrer">
                        / Page <i class="bi-link-45deg"></i>
                    </a>
                </small>
            </div>
        </a>
    </div>
    <div v-else-if="error" class="card">
        <h1>Error loading repos :/</h1>
        <p>{{error}}</p>
    </div>
    <h1 v-else class="card">loading repos...</h1>
</template>

<script>
export default {
    data() {
        return {
            repos: [],
            error: null
        }
    },
    mounted() {
        fetch('https://api.github.com/users/dzshn/repos').then(
            response => {
                if (response.ok) {
                    response.json().then(json => {this.repos = json})
                }
                else {this.error = `HTTP Error: ${response.status} ${response.statusText}!`}
            }
        ).catch(
            error => {this.error = error}
        )
    }
}
</script>

<style scoped lang="stylus">
#componentRoot
    @media screen and (min-width 600px)
        display flex
        flex-wrap wrap

    justify-content space-around
    align-items center
    text-align initial

div.card
    transition-duration 300ms
    min-width 30%
    max-width 600px
    &:hover
        scale 1.05
        background linear-gradient(to right, #333, #2a2a2a)
        h2
            background linear-gradient(to right, #454545, #555)

    @media screen and (max-width 600px)
        width 90%

h2
    background linear-gradient(to right, #353535, #444)
    padding 6px 7px 3px
    border-radius 8px
    width fit-content
</style>