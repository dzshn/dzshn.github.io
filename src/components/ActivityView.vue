<template>
    <div v-if="activity.length > 0" class="card">
        <ul>
            <li v-for="event in activity" :key="'a-'+event.id">
                <span v-if="event.type == 'PushEvent' && event.payload.commits.length == 1">
                    commited
                    <a :href="`https://github.com/${event.repo.name}/commit/${event.payload.commits[0].sha}`" target="_blank" rel="noopener noreferrer">
                        "{{event.payload.commits[0].message.split('\n')[0]}}"
                    </a>
                    to
                    <a :href="'https://github.com/'+event.repo.name" target="_blank" rel="noopener noreferrer">
                        {{event.repo.name}}
                    </a>
                </span>
                <span v-else-if="event.type == 'PushEvent'">
                    pushed {{event.payload.commits.length}} commits to
                    <a :href="'https://github.com/'+event.repo.name" target="_blank" rel="noopener noreferrer">
                        {{event.repo.name}}
                    </a>
                </span>
                <span v-else-if="event.type == 'CreateEvent'">
                    created {{event.payload.ref_type == 'branch'? 'a branch '+event.payload.ref+' on' : ''}}
                    <a :href="'https://github.com/'+event.repo.name" target="_blank" rel="noopener noreferrer">
                        {{event.repo.name}}
                    </a>
                </span>
                <span v-else-if="event.type == 'WatchEvent'">
                    starred
                    <a :href="'https://github.com/'+event.repo.name" target="_blank" rel="noopener noreferrer">
                        {{event.repo.name}}
                    </a>
                </span>
            </li>
        </ul>
    </div>
    <div v-else-if="error" class="card">
        <h1>Error loading activity :/</h1>
        <p>{{error}}</p>
    </div>
    <h1 v-else class="card">loading activity...</h1>
</template>

<script>
export default {
    data() {
        return {
            activity: [],
            error: ''
        }
    },
    mounted() {
        fetch('https://api.github.com/users/dzshn/events').then(
            response => {
                if (response.ok) {
                    response.json().then(json => {this.activity = json})
                }
                else {this.error = `HTTP Error: ${response.status} ${response.statusText}!`}
            }
        ).catch(
            error => {this.error = error}
        )
    }
}
</script>

<style scoped>
ul {
    height: 120px;
    overflow: scroll;
    overflow-x: hidden;
    padding: 0 20px 10px;
    background-color: #fff1;
    border-radius: 5px;
}

h3 {
    padding-left: 20px;
}
</style>