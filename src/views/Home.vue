<template>
        <div class="Home">
            <div class="feature_card">
                <router-link to="/movie/tt2975590">
                    <img src="https://www.teahub.io/photos/full/220-2205714_get-the-latest-movies-data-src-kodi-tv.jpg" alt="SPIDERMAN Poster" class="feature-img">
                    <div class="detail">
                        <h3>Movie</h3>
                        <p>Movies move us like nothing else can, whether they’re scary, funny, dramatic, romantic or anywhere in-between. So many titles, so much to experience.
                        </p>
                    </div>
                </router-link>
            </div>
            <form @submit.prevent="searchmovie()" class="search-box">
                <input type="text" placeholder="What are you looking for?" v-model="search"/>
                <input type="submit" value="Search">
            </form>

            <div class="movies-list">

                <div class="movie" v-for="movie in movies" :key="movie.imdbID">
                    <router-link :to="'/movie/'+ movie.imdbID" class="movie-link">
                        <div class="product-image">
                            <img :src="movie.Poster" alt="MoviePoster"/>
                            <div class="type">{{movie.Type}}</div>
                        </div>
                            <p class="year">{{movie.Year}}</p>
                            <h3>{{movie.Title}}</h3>

                    </router-link>
                </div>
            </div>
        </div>
</template>

<script>
    import {ref} from 'vue';
    import env from "../env";

    export default {
        setup() {
            const search = ref("");
            const movies = ref([]);

            const searchmovie = () => {
                if (search.value !== "") {
                    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
                        .then(response => response.json())
                        .then(data => {
                            movies.value = data.Search;
                            search.value = "";


                        });
                }
            }


            return {search, movies, searchmovie}
        }
    }
</script>


<style lang="scss">
    .Home {
        .feature_card {
            position: relative
        }

        .feature-img {
            display: block;
            width: 100%;
            height: 300px;
            object-fit: cover;
            position: relative;
            z-index: 0;
        }

        .detail {
            position: absolute;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.66);
            padding: 16px;
            z-index: 1;

        }

        h3 {
            color: #FFFFFF;
            margin-bottom: 16px;
        }

        p {
            color: #FFFFFF;
        }

        .search-box {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 16px;

            input {
                display: block;
                appearance: none;
                border: none;
                outline: none;
                background: none;

                &[type="text"] {
                    width: 100%;
                    color: #FFFFFF;
                    background-color: #496583;
                    font-size: 20px;
                    padding: 10px 16px;
                    border-radius: 8px;
                    margin-bottom: 15px;
                    transition: 0.4s;

                    &::placeholder {
                        color: #FFFFFF;

                    }

                    &:focus {
                        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
                    }
                }

                &[type="submit"] {
                    width: 100%;
                    max-width: 300px;
                    background-color: #42B883;
                    padding: 16px;
                    border-radius: 8px;
                    color: #FFFFFF;
                    font-size: 20px;
                    text-transform: uppercase;
                    transition: 0.4s;

                    &:active {
                        background-color: #3B8070;
                    }
                }

            }

        }

        .movies-list {
            display: flex;
            flex-wrap: wrap;
            margin: 0 8px;


            .movie {
                max-width: 50%;
                flex: 1 1 50%;
                padding: 16px 8px;


                .movie-link {
                    display: flex;
                    flex-direction: column;
                    height: 100%;


                    .product-image {
                        position: relative;
                        display: block;


                        img {
                            display: block;
                            width: 100%;
                            height: 275px;
                            object-fit: cover;
                        }

                        .type {
                            position: absolute;
                            padding: 8px 16px;
                            background-color: #42B883;
                            color: #ffffff;
                            bottom: 16px;
                            left: 0;
                            text-transform: capitalize;
                        }
                    }



                        .year {
                            color: #aaa;
                            background-color: #496583;
                            padding: 10px 10px 1px 8px;
                            flex: 1 1 100%;

                            font-size: 14px;
                        }

                        h3 {
                            color: #ffffff;
                            font-weight: 600;
                            background-color: #496583;
                            padding: 5px 8px 5px 8px;
                            flex: 1 1 100%;
                            border-radius: 0 0 8px 8px;
                            font-size: 18px;
                        }

                }
            }


        }
    }


</style>
