<template>
    <div>
        <Gallery @load-more="handleLoadMore" @toggle-comparison="addOrRemoveComparison" :images="relevantImages" :comparisonList="imageIdAddedToComparisonList"/>
        <Table :images="imagesAddedToComaparisonList"/>
    </div>
</template>

<script>
import Gallery from '@/components/Gallery.vue';
import Table from '@/components/Table.vue';
import axios from 'axios'

export default {
    name: 'Home-Page',
    components: {
        Gallery,
        Table
    },
    data(){
        return{
            allImagesFromEndpoint: [],
            showImageOnLoad: 10,
            imageIdAddedToComparisonList: [],
            imagesAddedToComaparisonList:[]
        }
    },
    computed:{
        //Function decide which images to show
        relevantImages(){
            return this.allImagesFromEndpoint.slice(0, this.showImageOnLoad)
        }
    },
    methods:{
        //Handle event on load more button click
        handleLoadMore(){
            this.showImageOnLoad += 5
        },
        //Add or remove images from comparison table
        addOrRemoveComparison(id){
            if(this.imageIdAddedToComparisonList.includes(id)){
                this.imageIdAddedToComparisonList = this.imageIdAddedToComparisonList.filter((c) => c !== id)
                this.imagesAddedToComaparisonList = this.imagesAddedToComaparisonList.filter((img=>img.id !== id))
            }
            else{
                this.imageIdAddedToComparisonList.push(id)
                let oi = this.relevantImages.findIndex((img=>img.id==id))
                this.imagesAddedToComaparisonList.push(this.relevantImages[oi])
            }
        }
    },
    async created(){
        //Fetching all the images from endpoint
        let response = await axios.get('https://jsonplaceholder.typicode.com/photos')
        if(response.status == 200)
            this.allImagesFromEndpoint = response.data
    }
};
</script>