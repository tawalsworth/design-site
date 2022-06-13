<template>

 <div class="parentColumn">
   
  <ul class="images imageSet">
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

export default {
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
.portfolio-grid {
  display: grid;
  margin-top: var(--section-spacing-2);
  grid-template: 1fr / 1fr;
  grid-gap: var(--section-spacing-1);
  width: 100%;
  height: 100%;
}


.image{
  display: inline-block;
  width: 300px;
}

.parentColumn {
    width: 100%;
    max-width: 1200px;
    display: grid;
    margin-top: var(--section-spacing-2);
    grid-template: 1fr / 1fr;
    grid-gap: var(--section-spacing-1);
    width: 100%;
    height: 100%;
    }
    ul {
    margin: 0;
    list-style: none;
    padding: 0;
     
    };
  .imageSet ::after {
    display: inline-block;
    display: grid;
        /* margin-top: 30px; */
    margin-top: var(--section-spacing-2);
    grid-template: 2fr 2fr / 2fr 2fr;
    grid-template-rows: 2fr 2fr;
    grid-template-columns: 2fr 2fr;
    grid-template-areas: none;
    }
    
</style>