<template>
    <div id="app">
        <div class="container">
            <app-header></app-header>
            <app-body
                :searchResults="searchResults"
                :repositoriesToCompare="repositoriesToCompare"
                :searchQuery="searchQuery"
            ></app-body>
        </div>
    </div>
</template>

<script>
    import { EventBus } from './main';
    import AppHeader from './components/app-header';
    import AppBody from './components/app-body';

    export default {
        name: 'App',
        components: {
            AppHeader,
            AppBody
        },
        data() {
            return {
                searchResults: [],
                repositoriesToCompare: [],
                searchQuery: ''
            }
        },
        created() {
            EventBus.$on('add-results', (data, searchQuery) => {
                if (data) {
                    this.searchResults = data.items;
                }

                this.searchQuery = searchQuery;
                this.repositoriesToCompare = [];
            });

            EventBus.$on('clear-results', () => {
                this.searchResults = [];
            });

            EventBus.$on('add-repository-to-compare', repository => {
                this.repositoriesToCompare.push(repository);
            });

            EventBus.$on('remove-repository-from-compare', id => {
                this.repositoriesToCompare = this.repositoriesToCompare.filter(repository => repository.id !== id);
            });
        }
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        font-family: -apple-system, 'Segoe UI', sans-serif;
        background-color: #edeef0;
    }

    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 0 15px;
    }
</style>
