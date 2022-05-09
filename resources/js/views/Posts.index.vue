<template>

    <!-- Section posts index -->
    <section class="posts_index container py-4 px-4">

        <!-- Grid container posts cards wrapper -->
        <div class="posts_cards_wrapper grid grid-cols-1 md:grid-cols-3 lg:grid:cols-4 sm:grid-cols-2 gap-16">
            <!-- Componente card post -->
            <PostCard v-for="element in postsArray" :key="element.id" :arrayPosts="element"/>
        </div>

    </section>

</template>

<script>
import Axios from "axios";

// Import post card
import PostCard from '../components/CardPost.vue';

export default {
    components: {
        PostCard
    },

    data() {
        return {

            // Array posts
            postsArray: [],
        }
    },

    methods: {

        // Funzione chiamata axios per recuperare i dati dei posts
        recuperoPosts: function() {

            // Axios
            Axios.get('http://127.0.0.1:8000/api/posts')
            .then( res => {

                // Recupero la risposta
                const {posts} = res.data;

                // Pusho i la risposta nell'array posts
                this.postsArray = posts;
            })
            .catch( err => {
                console.warn(err);
            })
        }
    },

    mounted() {

        // Richiamo la funzione recuperoPosts
        this.recuperoPosts();
    }
}
</script>

<style lang="sass" scoped>

</style>