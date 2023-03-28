<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
    name: "vite-yu-gi-oh",
    components: {
        AppHeader,
        AppMain,
    }
}
</script>

<template>
    <AppHeader />
    <AppMain />
</template>

<style lang="scss" scoped>
@import "./assets/main.scss";
</style>

