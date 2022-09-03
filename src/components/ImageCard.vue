<template>
    <div class="card">
        <div class="card__image">
            <img :src="image.thumbnailUrl" alt="picture image">
        </div>
        <h4 class="card__title">{{image.title}}</h4>
        <p> {{image.id}} </p>
        <p class="card__url"> {{image.url}} </p>
        <button @click="emitToggleCompare(image.id)" id="compare">{{isInComparison?'Remove':'Compare'}}</button>
    </div>
</template>

<script>

export default {
    name: 'Image-Card',
    props:["image", "isInComparison"],
    methods:{
        //Emit event to toggle images
        emitToggleCompare(id){
            this.$emit('toggle-compare', id)
        }
    }
};
</script>
<style scoped lang="scss">

.card {
  height: 300px;
  width: 250px;
  border: 1px solid;
  display: flex;
  flex-direction: column;
  align-items: center;
  
  &__image {
    max-width: 150px;
   max-height: 150px;
    img {
      width: 100%;
      height: 100%;
    }
  }
  
  &__title {
    overflow: hidden;
    text-align: center;
   text-overflow: ellipsis;
   display: -webkit-box;
   -webkit-line-clamp: 1; /* number of lines to show */
           line-clamp: 1; 
   -webkit-box-orient: vertical;
    margin: 0;
    padding: 0;
  }

  &__url {
    font-size: 12px;
  }
  
  p {
    margin: 0;
  }
  
  * + * {
    margin-top: 10px;
  }
}
</style>