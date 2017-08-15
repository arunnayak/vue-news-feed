<template>
<div class="sourceselection">
    <h2 class=""></h2>
    <select class="form-control" v-on:change="sourceChanged">
        <option v-bind:value="source.id" v-for="source in sources">
            {{source.name}}
        </option> 
    </select>
    <div v-if="source">
        <h6>{{source.description}}</h6>
        <a v-bind:href="source.url" target="_blank">Go to {{source.name}} website</a>
    </div>
</div>  
</template>
<script>
export default {
  name: 'sourceselection',
  data () {
    return {
      sources: [],
      source: ''
    }
  },
  methods: {
    sourceChanged: function (e) {
      for (var i = 0; i < this.sources.length; i++) {
        if (this.sources[i].id === e.target.value) {
          this.source = this.sources[i]
        }
      }
      this.$emit('sourceChanged', e.target.value)
    }
  },
  created: function () {
    this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then(response => {
        this.sources = response.data.sources
      })
  }
}
</script>
<style scoped>

</style>



