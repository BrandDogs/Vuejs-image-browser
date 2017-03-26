<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<h2>Image viewer</h2>
		<div class="modal" v-bind:class="{active : modal}">
			<div class="modal-background"></div>
			<div class="modal-card">
				<header class="modal-card-head">
					<p class="modal-card-title">Image selector</p>
					<button class="delete" v-on:click="modal = false;"></button>
				</header>
				<section class="modal-card-body">
					<div class="pictures">
						<picture
							v-for="(item, index) in images"
							v-bind:item="item"
							v-bind:index="index"
							v-bind:key="item.id"
							v-on:image_selected="imageSelected"
							v-on:image_deselected="imageDeselected"
						>
						</picture>
					</div>
					<!-- Content ... -->
				</section>
				<footer class="modal-card-foot">
					<a class="button is-success" v-on:click="modal = false;">Save changes</a> <a class="button" v-on:click="resetState">Cancel</a>
				</footer>
			</div>
		</div>
		<button class="button is-primary" v-on:click="activateModal">Select images</button>
		<div class="selectedImages" v-if="selectedImages.length > 0">
			<hr>
			<h3 class="title is-1">Selected images({{selectedImages.length}})</h3>
			<ul class="selected-images-list">
				<li class="selected-image-list-item" v-for="image in selectedImages">
					<span class="image-title" v-text="image.title"></span> <img :src="image.url" :alt="image.title">
				</li>
			</ul>
		</div>
	</div>
</template>
<script>

import Vue from 'vue'

import Picture from './Picture'


export default {

  components:{
    Picture
  },
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      images: [

        {'id':1, 'title':'image-1', 'url': '/static/boot-holland.png'},
        {'id':2, 'title':'image-2', 'url': '/static/eisenga-case.jpg'},
        {'id':3, 'title':'image-2', 'url': '/static/fijnproevers.jpg'}

      ],

      selectedImages:[],

      modal:false
    }
  },

  methods:{

    activateModal(){
      let that = this;

      if(that.modal){
        that.modal = false;
      }else{
        that.modal = true;
      }

    },

    imageSelected(image) {
      this.selectedImages.push(image)
    },

    imageDeselected(image, index) {
      this.selectedImages.splice(this.index, 1)
    },
    
    resetState(){
    	let that = this;
			
	    that.modal = false;
	    that.selectedImages = [];

	    for (let image of that.$children) {
		    image.selected = false;
	    }
    }

  }
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ul {
  list-style-type: none;
  padding: 0;
}

.selected-images-list{
  display: flex;
  flex-direction: column;
}

.selected-image-list-item{
  flex:1 0 auto;
}

.selected-image-list-item > img{
  width:50px;
  height: auto;

}

.pictures{
  display:flex;
}

.modal.active{
  display:block;
}


</style>
