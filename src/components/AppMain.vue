<script>
import axios from 'Axios'
export default {
    name: 'AppMain',
    data() {
        return {
            api_url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php',
            error: false,
        }
    },
    mounted() {
        axios
            .get(this.api_url)
            .then((response) => {
                console.log(response.data);
            })
            .catch((error) => {
                console.error(error);
            })
    }

}
</script>

<template>
    <main>
        <h1>main</h1>
    </main>
</template>


<style scoped></style>