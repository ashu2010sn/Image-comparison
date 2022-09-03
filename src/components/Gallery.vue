<template>
    <div class="gallery">
        <ImageCard v-for="image in images" :key="image.id" :image="image" :isInComparison="comparisonList.includes(image.id)" @toggle-compare="propogateToggleComparison"/>
        <button @click="emitLoadMore" class="load-more"> Load More </button>
    </div>
</template>

<script>
import ImageCard from './ImageCard.vue';
export default {
    name: "Gallery-Component",
    props: {
        images: {
            type: Array,
            default: () => []
        },
        comparisonList: {
            type: Array,
            default: () => []
        }
    },
    components: {
        ImageCard
    },
    methods:{
        //Asking parent to load more images
        emitLoadMore(){
            this.$emit("load-more")
        },
        //Forwarding toggle comparison
        propogateToggleComparison(id){
            this.$emit('toggle-comparison', id)
        }
    }
};
</script>
<style>
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(10rem, 1fr));
    grid-gap: 1rem;
    max-width: 80rem;
    margin: 5rem auto;
    padding: 0 5rem;
  }
  .load-more{
    width: 200px;
    color: #fff;
    display: block;
    text-align: center;
    margin: 20px auto;
    padding: 10px;
    border-radius: 10px;
    border: 1px solid transparent;
    background-color: blue;
    transition: .3s;
  }
</style>