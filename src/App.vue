
<template>
 
  <ul class="images">
    <li
      v-for="image in images"
      v-bind:key="image.sys.id"
      class="image"
    > 
        <div class="image-info">
          <div class="">{{ image.imageTitle }}
          test</div>
         <div class="image-name">
           <p></p>
         </div>
         <div class="image-content">
           <!-- <p class="image-theater">{{ images.imageTitle }} test 2</p>
           <p class="image-location">{{ image.postTime }} test 3</p> -->
         </div>
       </div>



    </li>
  </ul>

</template>


<script>
// import Shows from "./components/Shows.vue";
// import Hero from "./components/Hero.vue";
export default {
  data() {
    return {
        images: []
      };
  },
  components: {
    // Shows,
    // Hero
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

body {
  margin: 0;
  font-family: "Verdana";
  background-color: purple;
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
</style>