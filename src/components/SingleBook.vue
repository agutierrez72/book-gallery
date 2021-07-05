<template>
  <div class="book">
    <img class=" image h-28 place-self-center" :src="imageSrc">
    <h2>{{ book.title }}</h2>
    <h4>{{book.author}}</h4>
    <p>{{ book.description }}</p>
  </div>
</template>

<script>
export default {
    props: ['book'],
    computed: {
        imageSrc(){
            return require('../assets/'+this.book.image)
        }
    }

}
</script>

<style>

</style>