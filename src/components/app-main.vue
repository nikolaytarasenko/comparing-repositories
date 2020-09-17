<template>
    <main class="app-main">
        <app-form></app-form>
        <app-results
            :searchResults="searchResults"
            :repositoriesToCompare="repositoriesToCompare"
            :searchQuery="searchQuery"
        ></app-results>
    </main>
</template>

<script>
    import AppForm from './app-form';
    import AppResults from './app-results';

    export default {
        props: {
            searchResults: Array,
            repositoriesToCompare: Array,
            searchQuery: String
        },
        components: {
            AppForm,
            AppResults
        }
    }
</script>

<style scoped>
    .app-main {
        flex: 0 1 48%;
    }
</style>
