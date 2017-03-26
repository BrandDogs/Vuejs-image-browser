<template>

  <figure class="picture" v-on:click="clickImage(item, index)" v-bind:class="{active: isItemSelected(item)}">

    <img :src="item.url">
    <figcaption>{{item.title}}</figcaption>
  </figure>

</template>

<script>


export default {
  name:'picture',

  props:['item','index'],

  data () {
    return {

        selected:false

    }
  },

  methods:{

    clickImage(image, index){

      let that = this;

      if(that.selected == false){

        that.selected = true;

        this.$emit('image_selected', image)

      }else{

        that.selected = false;
        this.$emit('image_deselected')



      }


    },

    isItemSelected(item){
      let that = this;

      if(that.selected){

        return true;
      }else{


        return false;
      }
    },



  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .picture{
    flex:1 33%;
    box-sizing: border-box;
    color: #171e42;
    padding: 10px;
  }

  .picture.active{

    background:#333;
    color:#fff;

  }

  img{
    max-width: 100%;
    height:auto;
  }

</style>
