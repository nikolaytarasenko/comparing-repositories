<template>
    <div class="app-results">
        <h3 class="app-results-count">
            <span v-if="!getSearchResultsLength">No results.</span>
            <span v-else>Results for "{{ searchQuery }}": {{ getSearchResultsLength }} (limit: 30)</span>
        </h3>
        <div class="preloader" v-if="isLoading">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
        </div>
        <div class="app-results-body">
            <div class="app-results-row" v-for="result in searchResults" :key="result.id">
                <div class="app-results-info">
                    <p>Repository: <a class="app-results-link" :href="result.html_url" target="_blank">{{ result.name }}</a></p>
                    <p>Author: <a class="app-results-link" :href="result.owner.html_url" target="_blank">{{ result.owner.html_url }}</a></p>
                </div>
                <div class="app-results-buttons">
                    <button
                        type="button"
                        class="app-remove-btn"
                        v-if="repositoriesToCompare.some(repo => repo.id === result.id)"
                        @click="removeRepositoryFromCompare(result.id)"
                    >remove</button>
                    <button
                        type="button"
                        class="app-add-btn"
                        v-else
                        @click="addRepositoryToCompare(result)"
                    >add to compare</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { EventBus } from '../main';

    export default {
        props: {
            searchResults: {
                type: Array,
                default: () => {
                    return [];
                }
            },
            repositoriesToCompare: {
                type: Array,
                default: () => {
                    return [];
                }
            },
            searchQuery: {
                type: String,
                default: () => {
                    return '';
                }
            }
        },
        data() {
            return {
                isLoading: false
            }
        },
        computed: {
            getSearchResultsLength() {
                return this.searchResults.length;
            },
            getSearchQueryLength() {
                return this.searchQuery.length;
            }
        },
        created() {
            EventBus.$on('display-preloader', bool => {
                this.isLoading = bool;
            })
        },
        methods: {
            addRepositoryToCompare(repository) {
                EventBus.$emit('add-repository-to-compare', repository);
            },
            removeRepositoryFromCompare(id) {
                EventBus.$emit('remove-repository-from-compare', id);
            }
        }
    }
</script>

<style scoped>
    .app-results {
        position: relative;
        margin-bottom: 50px;
        color: #1a4b78;
    }

    .app-results-count {
        margin: 10px 0;
        font-weight: 400;
    }

    .app-results-row {
        display: flex;
        justify-content: space-between;
        align-items: center;
        word-break: break-all;
        font-size: 13px;
        padding: 10px;
        border: 1px solid #dcdcdc;
        background-color: #ffffff;
        border-radius: 3px;
    }

    .app-results-row:not(:last-child) {
        margin-bottom: 20px;
    }

    .app-results-link {
        color: #597ba0;
        text-decoration: none;
        font-weight: bold;
    }

    .app-results-info {
        flex: 1;
    }

    .app-results-info p {
        margin-bottom: 10px;
    }

    .app-add-btn,
    .app-remove-btn {
        background: transparent;
        cursor: pointer;
        padding: 1px 7px 3px;
        font-family: inherit;
        border-radius: 3px;
        transition: 0.1s ease;
    }

    .app-add-btn {
        border: 2px solid #41B883;
        color: #41B883;
    }

    .app-add-btn:hover {
        background: #41B883;
        color: #ffffff;
    }

    .app-remove-btn {
        border: 2px solid #da4f4f;
        color: #da4f4f;
    }

    .app-remove-btn:hover {
        background: #da4f4f;
        color: #ffffff;
    }

    .app-add-btn:focus,
    .app-add-btn:active,
    .app-remove-btn:focus,
    .app-remove-btn:active{
        outline: 0;
    }

    .app-results-buttons {
        flex-basis: 120px;
        text-align: right;
    }

    /* preloader */
    .preloader {
        display: block;
        position: absolute;
        top: 70%;
        left: 50%;
        transform: translate(-50%, -30%);
        height: 50px;
        width: 50px;
    }

    .preloader span {
        position: absolute;
        display: block;
        bottom: 10px;
        width: 9px;
        height: 5px;
        background: rgba(0, 0, 0, 0.25);
        animation: preloader 1.5s  infinite ease-in-out;
    }

    .preloader span:nth-child(2) {
        left: 11px;
        animation-delay: 0.2s;
    }

    .preloader span:nth-child(3) {
        left: 22px;
        animation-delay: 0.4s;
    }

    .preloader span:nth-child(4) {
        left: 33px;
        animation-delay: 0.6s;
    }

    .preloader span:nth-child(5) {
        left: 44px;
        animation-delay: 0.8s;
    }

    @keyframes preloader {
        0% {
            height: 5px;
            transform: translateY(0);
            background: rgba(0, 0, 0, 0.25);
        }
        25% {
            height: 30px;
            transform: translateY(15px);
            background: #41B883;
        }
        50% {
            height: 5px;
            transform: translateY(0);
            background: rgba(0, 0, 0, 0.25);
        }
        100% {
            height: 5px;
            transform: translateY(0);
            background: rgba(0, 0, 0, 0.25);
        }
    }
</style>
