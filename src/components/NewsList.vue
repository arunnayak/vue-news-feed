<template>
<div class="newslist">
    {{source}}
     {{articles}}
    <ul>
        <li v-for="atricle in articles">
            <a  v-bind:href="atricle.url" target="_blank">
                <img v-bind:src="article.urlToImage"  />
            </a>
            <a  v-bind:href="atricle.url" target="_blank">
                {{article.title}}
            </a>
            <p>by {{article.author}}</p>
            <p>{{article.description}}</p>
        </li>
    </ul>
</div>  
</template>
<script>
export default {
  name: 'newslist',
  props: ['source'],
  data () {
    return {
      articles: []
    }
  },
  methods: {
    updateSource: function (source) {
      this.$http.get('https://newsapi.org/v1/articles?source=bloomberg&apiKey=05b088d7ecf645808a38ba1150b90a42')
      .then(response => {
        this.articles = response.data.articles
      })
    }
  },
  created: function () {
    this.updateSource(this.source)
  },
  watch: {
    source: function (val) {
      this.updateSource(val)
    }
  }
}
</script>
<style scoped>

</style>



