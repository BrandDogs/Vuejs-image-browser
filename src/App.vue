<template>
  <div id="app">
    <img src="./assets/logo.png">
    <image-viewer v-on:save="syncSelectedImages"></image-viewer>
  </div>
</template>

<script>

import Picture from './components/Picture'
import ImageViewer from './components/ImageViewer'

export default {
  name: 'app',
  components: {
    ImageViewer
  },
	data () {
		return {

			selected:[]

		}
	},
  methods:{

	  syncSelectedImages(images){

	  	this.selected = [];

	  	this.selected.push(images);

    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
