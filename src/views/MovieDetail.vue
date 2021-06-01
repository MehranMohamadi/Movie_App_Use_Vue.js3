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
                fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}`)
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
    .Movie_Detail {
        padding: 16px;


        h2 {
            color: #ffffff;
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 16px;
        }

        .feature-img {
            display: flex;
            max-width: 200PX;
            margin-bottom: 16px;
            align-items: center;
        }

        p {
            color: #ffffff;
            font-size: 18px;
            line-height: 1.4;
        }
    }
</style>
