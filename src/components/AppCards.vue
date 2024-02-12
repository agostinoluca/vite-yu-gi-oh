<script>
export default {
    name: 'AppCards',
    props: {
        characters: {
            type: Array,
            required: false
        }
    }

}
</script>
        
<template>
    <div v-if="!characters">
        <p>Error loading API. The service may be temporarily unavailable.</p>
    </div>
    <div v-else class="col-12 col-sm-6 col-md-4 col-lg-2" v-for="character in characters"
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
</template>


<style scoped>
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