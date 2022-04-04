<template>
 <ul class="news__list">
     <div class="row">
        <div v-for="article in articles" class="col-4">
            <img v-bind:src="article.urlToImage" class="img-fluid">
            <h4>{{article.title}}</h4>
            <p>{{article.description}}</p>
        </div>
     </div>

 </ul>
</template>

<script>
export default {
    data() {
         return {
            articles: []
        }
    },
    created() {
        let self = this;

        fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
    headers: {
        Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
    }
})
    .then(function(response) {
        return response.json();
        })
        .then(function(data) {
            console.log(data);
            self.articles = data.articles;
        });
    }
}
</script>

<style>
    div.col-4{
        border: 1px solid;
        padding: 10px;
        box-shadow: 1px 1px 1px 1px;
    }
</style>