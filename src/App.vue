<template>
    <div class="app">
        <h3>
            A collective list of free APIs for use in <br />
            software and web development.
        </h3>
        <Search @text="searchText = $event" />
        <div class="container">
            <h4>Featured APIs of this week</h4>
            <div class="api-list" v-if="filteredApis.length > 0">
                <ApiItem
                    v-for="api in filteredApis"
                    :key="api.id"
                    :api="api"
                    @toggleBookmark="toggleBookmark(api.id)"
                />
            </div>
            <Alert v-else message="API not found" />
        </div>
        <div class="container">
            <h4>Your Bookmarks</h4>
            <div class="api-list" v-if="bookmarksApis.length > 0">
                <ApiItem
                    v-for="api in bookmarksApis"
                    :key="api.id"
                    :api="api"
                    @toggleBookmark="toggleBookmark(api.id)"
                />
            </div>
            <Alert v-else message="There is no item on your bookmarks" />
        </div>
    </div>
</template>

<script>
    import Search from "@/components/Search"
    import ApiItem from '@/components/ApiItem'
    import Alert from "@/components/Alert"

    import axios from "axios"

    export default {
        name: 'App',
        components: { Search, ApiItem, Alert },
        data() {
            return {
                apis: [],
                searchText: "",
            }
        },
        async created() {
            this.fetchAPIs()
        },

        methods: {
            async fetchAPIs() {
                const response = await axios.get(" http://localhost:5000/apis")
                this.apis = response.data
            },
            async fetchAPI(id) {
                const response = await axios.get(`http://localhost:5000/apis/${id}`)
                return response.data
            },
            async toggleBookmark(id) {
                const api = await this.fetchAPI(id)
                const updateBookmark = { ...api, bookmark: !api.bookmark }

                const response = await axios.put(`http://localhost:5000/apis/${id}`, updateBookmark)
                if (response.status === 200) {
                    this.apis = this.apis.map(api => api.id === response.data.id ? { ...api, bookmark: response.data.bookmark } : api)
                }
            },
        },
        computed: {
            filteredApis() {
                return this.apis.filter((api) => api.name.toLowerCase().includes(this.searchText.toLowerCase()))
            },
            bookmarksApis() {
                return this.apis.filter((api) => api.bookmark === true)
            }
        }
    }
</script>

<style lang="scss">
    @import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@300;400;500;600;700&display=swap");

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        border: none;
        text-decoration: none;
        list-style: none;
        font-family: "IBM Plex Sans", -apple-system, BlinkMacSystemFont, "Segoe UI",
            Roboto, "Helvetica Neue", Arial, sans-serif;

        &:focus {
            outline: none;
        }
    }
    body {
        background-color: #fafcfd;
        padding: 100px 0;
        text-align: center;

        h3 {
            font-size: 28px;
            color: #0e1238;
            margin-bottom: 50px;
        }

        .container {
            width: 1122px;
            max-width: 100%;
            margin: 0 auto 50px;
            text-align: left;

            > h4 {
                color: #151926;
                font-size: 22px;
                margin-bottom: 40px;
            }
            .api-list {
                display: flex;
                flex-wrap: wrap;
                margin: 0 -7px;
            }
        }
    }
</style>
