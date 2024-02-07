<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import AppFooter from './components/AppFooter.vue'
import AppLoader from './components/AppLoader.vue'
export default {
    name: 'App',
    components: {
        AppHeader,
        AppMain,
        AppFooter,
        AppLoader
    },
}
</script>

<template>
    <AppLoader></AppLoader>
    <AppHeader></AppHeader>
    <AppMain></AppMain>
    <AppFooter></AppFooter>
</template>

<style ></style>
