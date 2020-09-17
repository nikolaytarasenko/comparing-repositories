<template>
    <div class="app-table">
        <table>
            <tr>
                <th>Name</th>
                <th>Stars</th>
                <th>Forks</th>
                <th>Open issues</th>
            </tr>
            <tr v-for="repository in repositoriesToCompare" :key="repository.id">
                <td>{{ repository.full_name }}</td>
                <td>{{ repository.stargazers_count }}</td>
                <td>{{ repository.forks_count }}</td>
                <td>{{ repository.open_issues_count }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        props: {
            repositoriesToCompare: Array
        }
    }
</script>

<style scoped>
    .app-table {
        flex: 0 1 48%;
    }

    .app-table table {
        border-collapse: collapse;
        width: 100%;
        position: sticky;
        top: 10px;
    }

    .app-table th {
        background-color: #232323;
        color: #ffffff;
        padding: 10px;
        font-weight: 400;
    }

    .app-table td:not(:first-child) {
        text-align: center;
    }

    .app-table tr:not(:first-child) td {
        padding: 10px 0;
    }

    @media (max-width: 768px) {
        .app-table {
            overflow: scroll;
        }
    }
</style>
