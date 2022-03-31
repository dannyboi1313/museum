<template>
<div class="home">
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item.id">
      <h2>{{item.title}}</h2>
      <div class="pic">
        <img :src="item.path" />
      </div>
      <p>{{item.description}}</p>
      
    </div>
  </section>
</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
export default {
  name: 'Home',
    data() {
    return {
     items: [],
    }
  },
    created() {
    this.getItems();
  },
    methods: {
    async getItems() {
      try {
        let response = await axios.get("/api/items");
        this.items = response.data;
        return true;
      } catch (error) {
        console.log(error);
      }
    },
  }
}

</script>
<style scoped>
.image h2 {
  font-style: italic;
  text-align: center;
}
.image p{
  text-align: center;
}
.image img{
  max-height: 100px;
  max-width: 100px;
  margin-left: auto;
  margin-right: auto;
  
  
}
.pic{
  margin-left: auto;
  margin-right: auto;
  justify-content: center;
  width: 100px;
  height: 100px;
  
  
}
.image{
  
  align-content: center;
  width: 150px;
  height: 200px;
  border: solid black 2px;

}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  justify-content: center;
  align-content: center;
  width: 100%;
}



/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}
</style>
