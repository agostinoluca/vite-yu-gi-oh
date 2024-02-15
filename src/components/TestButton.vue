<script>
import { store } from '../store'
export default {
    name: 'TestButton',
    emits: ['bottone'],
    data() {
        return {
            store
        }
    },
}
</script>

<template>
    <div>
        <button class="btn btn-light" @click='store.increment'>You clicked me {{ store.count }} times</button>
        <!-- <button @click="$emit('bottone')">{{ store.count }}</button> -->
    </div>
</template>


<style scoped></style>