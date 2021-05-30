<template>
    <div class="Movie_Detail">
        <h2>{{movie.Title}}</h2>
        <p>{{movie.Year}}</p>
        <img :src="movie.Poster" alt="Movieposter" class="feature-img"/>
        <p>{{movie.Plot}}</p>
    </div>
</template>

<script>
    import {ref, onBeforeMount} from 'vue';
    import {useRoute} from 'vue-router';
    import env from "../env";

    export default {
        setup() {
            const movie = ref({});
            const route = useRoute();


            onBeforeMount(() => {
                fetch(`http://www/ombdapi.com/?apikey=${env.apikey}$i=${route.params.id}&plot
                =full`)
                    .then(response => response.json())
                    .then(data => {
                        movie.value = data;
                    });


            });

            return {movie}


        }
    }
</script>


<style lang="scss">

</style>
