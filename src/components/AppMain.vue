<script>
import axios from 'Axios'
export default {
    name: 'AppMain',
    data() {
        return {
            api_url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=150&offset=0',
            error: false,
            characters: [],
            select_options: [],
            selected_option: 'All',
        }
    },
    mounted() {
        axios
            .get(this.api_url)
            .then((response) => {
                this.characters = response.data.data;
                console.log(response.data.data[0].archetype);
                this.characters.forEach(character => {
                    if (!this.select_options.includes(character.archetype) && character.archetype.length > 0) {
                        this.select_options.push(character.archetype);
                    }
                });
            })
            .catch((error) => {
                console.error(error);
            })
    },
    computed: {
        filteredCharacters() {
            return this.selected_option === 'All' ? this.characters : this.characters.filter(character => character.archetype === this.selected_option);
        }
    }
}
</script>

<template>
    <main>
        <div class="container">
            <div class="row">
                <div class="col-12 m-1 mb-3">
                    <select class="form-select" name="filter" id="filter" style="width: auto;" v-model="selected_option">
                        <option value="All">All Cards Type</option>
                        <option v-for="option in select_options" :value="option">{{ option }}
                        </option>
                    </select>
                </div>
                <div class="col-12 col-sm-6 col-md-4 col-lg-2" v-for="character in filteredCharacters"
                    :key="character.id + '_character'">
                    <div class="card text-center mb-3">
                        <img :src="character.card_images[0].image_url" :alt="character.name + ' image'">
                        <div class="card-body d-flex flex-column justify-content-between">
                            <h5 class="card-title"> {{ character.name }}
                            </h5>
                            <h6 class="card-subtitle mb-2">{{ character.archetype }}</h6>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>


<style scoped>
main {
    padding-top: 6rem;
}

.card {
    background-color: rgba(0, 0, 0, 0.418);
    box-shadow: 0 0 0.25rem black;

    & .card-body {
        height: 10rem;
        color: white;
    }

    & img {
        border-radius: 0.5rem;
    }

    & h5 {
        text-transform: uppercase;
    }

    & h6 {
        color: rgb(192, 192, 192);
        font-weight: 400;
    }
}
</style>