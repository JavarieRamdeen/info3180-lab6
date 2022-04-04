<template>
 <ul class="news__list">
 <li class="news__item">News item 1</li>
 <li class="news__item">News item 2</li>
 <li class="news__item">News item 3</li>
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
        'Authorization': 'Bearer <d0b55a1e99df44eb89753c297fa5f7c4>'
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