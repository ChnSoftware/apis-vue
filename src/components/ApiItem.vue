<template>
    <div class="api-item">
        <div class="item-icon">
            <img :src="require(`../assets/icons/${api.icon}.svg`)" alt="" />
        </div>
        <div class="item-detail">
            <h4>{{ api.name }}</h4>
            <div class="item-category">{{ api.category }}</div>
            <div class="item-description">
                {{ api.description }}
            </div>
        </div>
        <div class="item-hover">
            <button @click="$emit('toggleBookmark', api.id)">
                <span v-if="api.bookmark">
                    <i class="fas fa-bookmark"></i>
                </span>
                <span v-else>
                    <i class="far fa-bookmark"></i>
                </span>
                Bookmark
            </button>
            <a :href="api.docs_url">
                API Docs
                <i class="fas fa-chevron-right"></i>
            </a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ApiItem",
        props: ["api"]
    }
</script>

<style lang="scss" scoped>
    .api-item {
        background-color: white;
        width: calc(100% / 3 - 14px);
        margin: 0 7px 14px;
        padding: 30px;
        display: flex;
        box-shadow: 0 20px 53px -30px rgba(#5f66ad, 0.57);
        position: relative;
        min-height: 210px;
        overflow: hidden;

        .item-icon {
            width: 64px;
            height: 64px;
            min-width: 64px;
            display: grid;
            place-items: center;
            margin-right: 25px;
        }
        .item-detail {
            h4 {
                font-size: 22px;
                color: #151926;
                margin-bottom: 5px;
            }
            .item-category {
                color: rgba(#151926, 0.7);
                font-size: 14px;
                margin-bottom: 10px;
            }
            .item-description {
                font-size: 16px;
                color: #151926;
                transition: 300ms opacity;
            }
        }
        .item-hover {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
            height: 88px;
            background-color: #f9fbfc;
            display: flex;
            align-items: center;
            padding: 0px 21px;
            transform: translateY(100%);
            transition: 300ms transform;

            a,
            button {
                flex: 1;
                margin: 0 9px;
                height: 40px;
                border-radius: 5px;
                display: flex;
                align-items: center;
                justify-content: center;
                font-size: 16px;
            }
            a {
                background-color: #141a31;
                color: #fff;

                svg {
                    width: 16px;
                    height: 16px;
                    margin-left: 5px;
                }
            }
            button {
                background-color: #fff;
                color: #141a31;
                cursor: pointer;

                svg {
                    width: 16px;
                    height: 16px;
                    margin-right: 5px;
                }
            }
        }
        &:hover {
            .item-hover {
                transform: translateY(0);
            }
            .item-detail {
                .item-description {
                    opacity: 0;
                }
            }
        }
    }
</style>