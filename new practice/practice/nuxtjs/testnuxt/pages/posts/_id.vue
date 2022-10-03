<template>
    <div class="container">
        <article>
            <h1>{{post.title}}</h1>
            <p>{{post.content}}</p>
        </article>
        <aside>
            <h2>Related Posts</h2>
            <div>
                <nuxt-link v-for="related in relatedPosts" :to="{name: 'posts-id', params: {id: related.id}}" :key="related.id">
                    {{related.title}}
                </nuxt-link>
            </div>
        </aside>
    </div>
</template>

<script>
   export default {
    data(){
        return {
            id: this.$route.params.id
        }
    },
    head() {
        return {
            title: this.post.title
        }
    },
    computed: {
        post() {
            return this.$store.state.posts.all.find(post => post.id === this.id)
        },
        relatedPosts(){
            return this.$store.state.posts.all.filter(post => post.id !== this.id)
        }
    }
   }
</script>