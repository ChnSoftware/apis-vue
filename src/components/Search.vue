<template>
    <form class="api-search-form" @keyup="$emit('text', text)">
        <div class="icon">
            <i class="fas fa-search"></i>
        </div>
        <input
            type="text"
            placeholder="Find development, games, images APIs"
            v-model="text"
        />
    </form>
</template>

<script>
    export default {
        name: "Search",
        data() {
            return {
                text: null
            }
        },
    }
</script>

<style lang="scss" scoped>
    .api-search-form {
        width: 720px;
        margin: 0px auto 70px;
        position: relative;

        .icon {
            position: absolute;
            top: 0;
            left: 20px;
            height: 80px;
            width: 70px;
            display: flex;
            align-items: center;
            justify-content: center;

            svg {
                height: 34px;
                width: 34px;
                color: #8e97b6;
            }
        }
        input {
            width: 100%;
            height: 80px;
            border: 1px solid #dfe8ed;
            border-radius: 40px;
            padding: 0 20px 0 90px;
            font-size: 18px;
            color: #6b7289;

            &::placeholder {
                color: #6b7289;
            }
        }
    }
</style>