<script>
export default {
    name: 'TestButton',
    emits: ['bottone']

}
</script>

<template>
    <div>
        <button @click="$emit('bottone')">Click</button>
    </div>
</template>


<style scoped></style>