<template>
    <div class="home">
        <div class="Home">
            <div class="feature_card">
                <router-link to="/movie/tt0409591">
                    <img src="https://wallpaperaccess.com/full/930271.jpg" alt="SPIDERMAN Poster" class="feature-img">
                    <div class="detail">
                        <h3>Spider-Man</h3>
                        <p>Peter Parker balances his life as an ordinary high school student in Queens with his
                            superhero alter-ego Spider-Man, and finds himself on the trail of a new menace prowling the
                            skies of New York City.
                        </p>
                    </div>
                </router-link>
            </div>
            <form @submit.prevent="searchmovie()" class="search-box">
                <input type="text" placeholder="What are you looking for?" v-model="search"/>
                <input type="submit" value="Search">
            </form>
            <div class="Movie-list">
                <div class="movie">
                    <div class="movie" v-for="movie in movies" :key="movie.imdbID">
                        <router-link :to="'/movie/'+movie.imdbID" class="movie-link">
                            <img :src="movie.Poster" alt="MoviePoster"/>
                            <div class="type">{{movie.Type}}</div>
                            <div class="detail">
                                <p class="year">{{movie.Year}}</p>
                                <h3>{{movie.Title}}</h3>
                            </div>
                        </router-link>
                    </div>
                </div>
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
                            movies.value = data.search;
                            search.value = '';
                            console.log(movies.value)
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

        .Movie-list {
            display: flex;
            flex-wrap: wrap;
            margin: 0 8px;
        }

        .movie {
            max-width: 50%;
            flex: 1 1 50%;
            padding: 16px 8px;


            .movie-link {
                display: flex;
                flex-direction: column;
                height: 100%;


                .prouduct-image {
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

                    .detail {
                        background-color: #496583;
                        padding: 16px 8px;
                        flex: 1 1 100%;
                        border-radius: 0 0 8px 8px;

                        .year {
                            color: #aaa;

                            font-size: 14px;
                        }

                        h3 {
                            color: #ffffff;
                            font-weight: 600;
                            font-size: 18px;
                        }
                    }

                }
            }
        }


    }


</style>
