<template>
    <div class="newsList">
        <div class="container">
            <ul class="media-list">
                <li class="media" v-for="(article, index) in articles" v-bind:key="index">
                    <div class="media-left">
                        <a v-bind:href="article.url" target="_blank">
                            <img class="media-object" v-bind:src="article.urlToImage"/>
                        </a>
                    </div>
                    <div class="media-body">
                        <h4 class="media-heading">
                            <a v-bind:href="article.url" target="_blank">{{ article.title }}</a>
                        </h4>
                        <h5><i>by {{ article.author }}</i></h5>
                        <p>{{ article.desciption }}</p>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'newsList',
    props:['source'],
    data() {
        return {
            articles: [],
        }
    },
    watch: {
        source: function(val) {
            this.updateSource(val);
        }
    },
    methods: {
        updateSource: function(source) {
            this.$http.get(`https://newsapi.org/v1/articles?source=${source}&apiKey=d6659badd609453d8c911a1aeb07bdde`)
            .then(response => {
                this.articles = response.data.articles;
            });
        }
    },
    created: function () {
        this.updateSource(this.source);
    }
}
</script>

<style scoped>
    .media-object {
        width: 128px;
        padding: 10px;
    }
    .media {
        border-top: 1px solid lightgray;
        padding-top: 20px;
    }
</style>
