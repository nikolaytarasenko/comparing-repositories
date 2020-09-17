<template>
    <header class="app-header">
        <div class="app-logo">
            <img :src="require('../assets/logo.png')" alt="logo">
        </div>
        <h1 class="app-title">Comparing Repositories</h1>
    </header>
</template>

<script>
    export default {}
</script>

<style scoped>
    .app-header {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 20px 0 40px;
    }

    .app-logo {
        margin-bottom: 10px;
    }

    .app-logo img {
        max-width: 50px;
    }

    .app-title {
        font-size: 32px;
        font-weight: 300;
        text-align: center;
    }
</style>
