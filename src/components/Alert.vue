<template>
    <div class="alert">{{ message }}</div>
</template>

<script>
    export default {
        name: "Alert",
        props: ["message"]
    }
</script>

<style lang="scss" scoped>
    .alert {
        background-color: #c3c5111c;
        padding: 20px;
        font-size: 16px;
        width: 100%;
        border-radius: 4px;
        text-align: left;
    }
</style>