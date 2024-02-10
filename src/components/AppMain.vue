<script>
import axios from 'Axios'
export default {
    name: 'AppMain',
    data() {
        return {
            api_url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0',
            error: false,
            characters: [],
        }
    },
    mounted() {
        axios
            .get(this.api_url)
            .then((response) => {
                console.log(response.data);
                this.characters = response.data.data;
                console.log(this.characters);
            })
            .catch((error) => {
                console.error(error);
            })
    }

}
</script>

<template>
    <main>
        <div class="container">
            <div class="row">
                <div class="col-12 col-sm-6 col-md-4 col-lg-2" v-for="character in characters"
                    :key="character.id + '_character'">
                    <div class="card text-center m-1 p-2">
                        <img :src="character.card_images[0].image_url" alt="">
                        <div class="card-body">
                            <h5 class="card-title"> {{ character.name }}
                            </h5>
                            <h6 class="card-subtitle mb-2">{{ character.type }}</h6>
                            <p>{{ character.archetype }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>


<style scoped>
.card {
    background-color: rgba(0, 0, 0, 0.418);

    & .card-body {
        height: 10rem;
        color: white;
    }

    & img {
        border-radius: 0.5rem;
    }
}
</style>