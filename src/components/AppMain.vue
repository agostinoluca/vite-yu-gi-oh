<script>
import axios from 'axios'
import AppLoader from './AppLoader.vue'
import AppCards from './AppCards.vue'
// import TestButton from './TestButton.vue'
export default {
    name: 'AppMain',
    components: {
        AppLoader,
        AppCards,
        // TestButton
    },
    data() {
        return {
            api_url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=750&offset=0',
            error: false,
            characters: [],
            loading: true,
            select_options: [],
            selected_option: 'All',
        }
    },
    methods: {
        getCharacters() {
            axios
                .get(this.api_url)
                .then((response) => {
                    this.characters = response.data.data;
                    this.loading = false;
                    // console.log(response.data.data[0].archetype);
                    this.characters.forEach(character => {
                        if (character.archetype && !this.select_options.includes(character.archetype)) {
                            this.select_options.push(character.archetype);
                            // console.log(character.archetype);
                        }
                    });
                    this.select_options.sort();
                })
                .catch((error) => {
                    console.error(error);
                })
        },
        // funzioneInventata() {
        //     console.log('funziono');
        // }
    },
    created() {
        // setTimeout(() => {
        this.getCharacters(this.api_url)
        // }, 3000);
    },
    computed: {
        filteredCharacters() {
            return this.selected_option === 'All' ? this.characters : this.characters.filter(character => character.archetype === this.selected_option);
        },
        getResults() {
            const cardCount = this.filteredCharacters.length;
            return this.filteredCharacters ? `Found ${cardCount} ${cardCount === 1 ? 'Card' : 'Cards'}` : 'No results yet';
        }
    },
}
</script>

<template>
    <main>
        <div class="container">
            <!-- <TestButton @bottone="funzioneInventata"></TestButton> -->
            <div class="row" v-if="!loading">
                <div class="col-12 mb-3 d-flex justify-content-between align-items-center">
                    <select class="form-select" name="filter" id="filter" style="width: auto;" v-model="selected_option">
                        <option value="All">
                            All Cards Archetype
                        </option>
                        <option v-for="option in select_options" :value="option">
                            {{ option }}
                        </option>
                    </select>
                    <div class="results">
                        {{ getResults }}
                    </div>
                </div>
                <AppCards :characters="filteredCharacters"></AppCards>
            </div>
            <AppLoader v-else></AppLoader>
        </div>

    </main>
</template>


<style scoped>
main {
    padding-top: 6rem;
}

.results {
    color: white;
    background-color: rgba(0, 128, 0, 0.562);
    padding: 0.5rem;
    border-radius: 1rem;
    box-shadow: 0 0 0.15rem rgba(255, 255, 255, 0.356);
}
</style>