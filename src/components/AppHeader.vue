<script>
export default {

}
</script>

<template>
    <header>
        <div class="d-flex align-items-center">
            <img width="80" src="/logo.png" alt="logo Yu-Gi-Oh">
            <span>Yu-Gi-Oh Api</span>
        </div>
    </header>
</template>


<style scoped>
header {
    width: 100%;
    background-color: white;
    padding: 1.5rem;
    box-shadow: 0 0 2rem black;
    position: fixed;
    z-index: 9999;

    & span {
        font-size: 2rem;
        font-weight: 500;
        margin-left: 1rem;
        line-height: 100%;
    }
}
</style>