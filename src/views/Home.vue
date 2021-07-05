<template>
  <div class="home">

      <!-- <div v-for="book in books" :key="book.id">  
        <SingleBook :book="book" />
      </div> -->
    <swiper
      :slides-per-view="3"
      :space-between="50"
      navigation
      :pagination="{ clickable: true }"
      @swiper="onSwiper"
      @slideChange="onSlideChange"
    >
      <swiper-slide v-for="book in books" :key="book.id"><SingleBook :book="book"/></swiper-slide>

      ...
    </swiper>
  </div>
</template>

<script>
// @ is an alias to /src
import {ref} from 'vue'
import SingleBook from '../components/SingleBook.vue'
import SwiperCore, { Navigation, Pagination, Scrollbar, A11y } from 'swiper'
import {Swiper, SwiperSlide} from 'swiper/vue'
import 'swiper/swiper-bundle.css'

SwiperCore.use([Navigation, Pagination, Scrollbar, A11y])

export default {
  name: 'Home',
  components: {
    SingleBook, Swiper, SwiperSlide

  },
  methods: {
    onSwiper(swiper) {
      console.log(swiper);
    },
    onSlideChange() {
      console.log('slide change');
    },
  },
  setup(){
    const books = ref([])
    const error = ref(null)

    const load = async () => {
      try {
        let data = await fetch('http://localhost:3000/books')
        console.log(data)
        if(!data.ok){
          throw Error('no data retrieved')
        }
        books.value = await data.json()
      } catch (err) {
        error.value = err.message
      }
    }

    load()

    return { books }
  }
}
</script>
