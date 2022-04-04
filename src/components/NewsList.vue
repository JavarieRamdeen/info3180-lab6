<template>
 <ul class="news__list">
    <form  @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm"
                id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
                <button class="btn btn-primary mb-2">Search</button>
        </div>
    <p>You are searching for {{ searchTerm }}</p>
 </form>
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
            articles: [],
            searchTerm: ''
        }
    },
    
    methods: {
        searchNews() {
            let self = this;
            fetch('https://newsapi.org/v2/everything?q='+self.searchTerm + '&language=en', {
                headers: {'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,}
            })
            .then(function(response) {
                return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles = data.articles;
            });
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
    },
}
</script>

<style>
    div.col-4{
        border: 1px solid;
        padding: 10px;
        box-shadow: 1px 1px 1px 1px;
    }
</style>