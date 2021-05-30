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
            <form @submit.prevent="" class="search-box">
                <input type="text" placeholder="What are you looking for?">
                <input type="submit" value="Search">
            </form>
            <div class="Movie-list">Movies</div>
        </div>
    </div>
</template>

<script>


    export default {}
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
    }
</style>
