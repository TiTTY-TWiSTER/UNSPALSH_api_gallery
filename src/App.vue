<template>
  <div id="app">
      <gallery-app></gallery-app>
  </div>
</template>

<script>
import Gallery from './gallery.vue'

import JQuery from 'jquery'
  let $ = JQuery

export default {
  name: 'app',
  data () {
    
  },
  components:{
    'gallery-app':Gallery,
  },
  mounted(){
    
  },
  methods:{
  },
}
</script>

<style>
img{
  max-width:100%;
}
</style>
