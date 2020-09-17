<template>
    <div class="app-body">
        <app-main
            :searchResults="searchResults"
            :repositoriesToCompare="repositoriesToCompare"
            :searchQuery="searchQuery"
        ></app-main>
        <app-table :repositoriesToCompare="repositoriesToCompare"></app-table>
    </div>
</template>

<script>
    import AppMain from './app-main';
    import AppTable from './app-table';

    export default {
        props: {
            searchResults: Array,
            repositoriesToCompare: Array,
            searchQuery: String
        },
        components: {
            AppMain,
            AppTable
        }
    }
</script>

<style scoped>
    .app-body {
        display: flex;
        justify-content: space-between;
    }

    @media (max-width: 768px) {
        .app-body {
            flex-direction: column;
        }
    }
</style>
