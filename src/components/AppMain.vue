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
            <div class="row" v-for="character in characters">
                <div class="col-12">
                    <img :src="character.card_images[0].image_url" alt="">
                    {{ character.name }}
                </div>
            </div>
        </div>
    </main>
</template>


<style scoped></style>