<template>
    <div v-if="activity.length > 0" class="card">
        <ul>
            <li v-for="event in activity" :key="'a-'+event.id">
                {{ formatEvent(event) }} <br>
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
        let handleResp = response => {
            if (response.ok) {
                response.json().then(
                    json => {
                        this.activity = this.activity.concat(json).sort(
                            (a, b) => new Date(b.created_at) - new Date(a.created_at)
                        )
                    }
                )
            } else {
                this.error = `HTTP Error: ${response.status} ${response.statusText}!`
            }
        }
        fetch('https://api.github.com/users/dzshn/events')
                .catch(error => {this.error = error})
                .then(handleResp)
        fetch('https://api.github.com/users/dzshn/received_events')
                .catch(error => {this.error = error})
                .then(handleResp)
    },
    methods: {
        formatEvent(e) {
            let user = e.actor.login
            let repo = e.repo.name
            e.payload.pull_request = e.payload.pull_request ?? {}
            e.payload.commits = e.payload.commits ?? {}
            e.payload.issue = e.payload.issue ?? {}
            const eventTemplates = {
                "CommitCommentEvent": `${user} commented on a commit in ${repo}`,
                "CreateEvent": `${user} created a ${e.payload.ref_type} on ${repo}`,
                "DeleteEvent": `${user} deleted a ${e.payload.ref_type} on ${repo}`,
                "ForkEvent": `${user} forked ${repo}!`,
                "GollumEvent": `${user} updated the wiki at ${repo}`,
                "IssueCommentEvent": `${user} commented on issue #${e.payload.issue.number} in ${repo}`,
                "IssuesEvent": `${user} ${e.payload.action} an issue in ${repo}`,
                "MemberEvent": `${user} updated a member on ${repo}`,
                "PublicEvent": `${user} changed ${repo} from private to public!`,
                "PullRequestEvent":
                    `${user} ${
                        ['opened', 'closed', 'reopened', 'assigned', 'unassigned']
                            .indexOf(e.payload.action) > -1?
                                e.payload.action :
                                'modified'
                    } a pull request on ${repo}`,
                "PullRequestReviewEvent":
                    `${user} ${e.payload.action} a PR review (#` +
                    `${e.payload.pull_request.number}) on ${repo}`,
                "PullRequestReviewCommentEvent":
                    `${user} ${e.payload.action} a comment on a PR review (#` +
                    `${e.payload.pull_request.number}) on ${repo}`,
                "PushEvent":
                    `${user} pushed ${
                        e.payload.commits.length > 1?
                            `${e.payload.commits.length} commits` :
                            'a commit'
                    } on ${repo}`,
                "ReleaseEvent": `${user} made a release on ${repo}`,
                "WatchEvent": `${user} starred ${repo}!`
            }

            return eventTemplates[e.type]
        }
    }
}
</script>

<style scoped lang="stylus">
ul
    background-color #fff1
    border-radius 5px
    height 120px
    overflow hidden scroll
    padding 0 20px 10px

button
    padding 0
    margin 0
    text-align right
</style>