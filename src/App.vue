<template>

 <div class="parentColumn">
   <header></header>
  <ul class="images">
    <li
      v-for="image in images"
      v-bind:key="image.sys.id"
      class="image"
    > 
      <img :src="image.galleyImage.url" />
        <div class="image-info">

            <img :src="image.galleryImage" />

         <div class="image-name">
           <div class="">{{ image.imageTitle }}
          test</div>
         </div>
         <div class="image-content">
           {{ image.postTime }}
         </div>
       </div>



    </li>
  </ul>
</div>
</template>


<script>
import Header from './components/Header.vue'

export default {
    components: {
     'header':Header
  },
  data() {
    return {
        images: []
      };
  },

  async created() {
    this.images = await this.getImages();
  },

  methods: {
    getImages: async () => {
      const query = `{
        imageCollection {
          items {
            sys {
              id
            }
            
            imageTitle
            postTime
            galleyImage{
              fileName
              url
            }
          }
        }
      }`;

      const fetchUrl = `https://graphql.contentful.com/content/v1/spaces/1s0vh88z19o5`;
      const fetchOptions = {
        method: "POST",
        headers: {
          Authorization: `Bearer sfA2xhxNtzxuxCYlfTGKvPqkfdTOPq_qBl3zgoilSis`,
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ query })
      };
      try {
        const response = await fetch(fetchUrl, fetchOptions).then(response =>
          response.json()
        );
        console.log(response.data.imageCollection.items);
        return response.data.imageCollection.items;
      } catch (error) {
        throw new Error("Could not receive the data from Contentful!");
      }

    }
    
  }
 };
</script>

<style>
img{
  max-height: 20%;
  max-width: 20%; 
}

body {
  margin: 0;
  font-family: "Verdana";
  background-color: whitesmoke;
  color: black;
}

/* @import "@/assets/styles/variables.scss";
* {
  box-sizing: border-box;
}

#app {
  background-color: $purple;
  border: 7px solid $black;
  box-shadow: 10px 10px 0 $black;
  border-radius: 7px 7px 7px 0;
  max-width: 1200px;
  margin: 50px auto;
  @media screen and (max-width: 1200px) {
    margin: 20px;
  }
}
ul {
  margin: 0;
  list-style: none;
  padding: 0;
  li {
    display: inline-block;
  }
} */

.parentColumn {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: flex-start;
    background-color: white;
    }
    ul {
    margin: 0;
    list-style: none;
    padding: 0;
     
    };
</style>