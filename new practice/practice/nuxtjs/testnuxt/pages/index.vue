<template>
    <div class="container">
        <h1>Hello world!</h1>
        <div>
            <h2>Posts</h2>
            <nuxt-link 
            v-for="post in posts"
            :to="{name: 'posts-id', params: {id: post.id}}"
            :key="post.id">
            {{post.title}}
            </nuxt-link>
        </div>
    </div>
</template>

<script>
   export default {
    head () {
        return {
            title: 'Home Page'
        }
    },
    computed: {
        posts(){
            return this.$store.state.posts.all
        }
    }
   }
</script>