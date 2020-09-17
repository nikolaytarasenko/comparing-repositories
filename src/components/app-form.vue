<template>
    <form class="app-form" @submit.prevent="searchRepositories">
        <div class="app-form-row">
            <input
                type="text"
                class="app-control"
                placeholder="Search by repository name and description"
                v-model="query"
            >
            <button
                type="submit"
                class="app-search-btn"
                :disabled="!getSearchQueryLength"
            >search</button>
        </div>
    </form>
</template>

<script>
    import { EventBus } from '../main';

    export default {
        data() {
            return {
                query: ''
            }
        },
        computed: {
            getSearchQueryLength() {
                return this.query.length;
            }
        },
        methods: {
            searchRepositories() {
                const url = 'https://api.github.com/search/repositories?q=' + this.query;

                EventBus.$emit('clear-results');
                EventBus.$emit('display-preloader', true);

                fetch(url)
                    .then(response => response.json())
                    .then(data => {
                        EventBus.$emit('display-preloader', false);
                        EventBus.$emit('add-results', data, this.query);
                        this.query = '';
                    }).catch(err => {
                        throw new Error(err);
                    });
            }
        }
    }
</script>

<style scoped>
    .app-form {
        background-color: #4c75a3;
        padding: 20px;
    }

    .app-form-row {
        display: flex;
    }

    .app-control {
        font-family: inherit;
        padding: 5px 10px;
        border: none;
        flex: 1;
        background: #31537a;
        color: #ffffff;
        border-radius: 15px;
    }

    .app-control::placeholder {
        color: #ffffff;
        opacity: 0.8;
    }

    .app-search-btn {
        margin-left: 20px;
        background:  #41B883;
        color: #ffffff;
        font-family: inherit;
        border: 0;
        padding: 5px 15px;
        cursor: pointer;
        text-transform: uppercase;
        border-radius: 15px;
        transition: 0.1s ease;
    }

    .app-search-btn:hover {
        background-color: #399e42;
    }

    .app-search-btn:disabled {
        opacity: 0.5;
        cursor: default;
    }

    .app-search-btn:disabled:hover {
        background:  #41B883;
    }

    .app-control:focus,
    .app-control:active,
    .app-search-btn:focus,
    .app-search-btn:active {
        outline: 0;
    }

    @media (max-width: 415px) {
        .app-form-row {
            flex-direction: column;
        }

        .app-search-btn {
            margin-left: 0;
            margin-top: 10px;
            align-self: center;
        }
    }
</style>
