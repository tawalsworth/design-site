<template>
<div class="inner-container ">
 <div class="portfolio-grid">
   
  <ul class="images justify-self-center imageSet grid md:gap-4 md:grid-cols-4 md:grid-rows-3">
    <li
      v-for="image in images"
      v-bind:key="image.sys.id"
      class="image mx-4 my-4"
    >

      <img :src="image.galleyImage.url" />
        
        <div class="image-info justify-self-center">
            <img :src="image.galleryImage" />
            <div class="inline-block tagBackground pt-2 pb-2">
                  <div class="image-name">
                    <div class="title">{{ image.imageTitle }}</div>
                  </div>
                  <div class="image-content">
                    <div class="time">
                      {{image.postTime}}
                    </div>
                  </div>
            </div>
       </div>

    </li>
  </ul>
  </div>
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

@import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;1,400&family=Poppins:wght@100;200;300;500&display=swap');

body {
  margin: 0;
  font-family: "Verdana";
  background-color: whitesmoke;
  color: black;
}

.title {
  font-family: 'DM Sans', sans-serif;
  font-size: 21px;
  text-align: center;
  font-weight: 300;
}

.time{
  font-family: 'DM Sans', sans-serif;
  font-size: 13px;
  text-align: center;
  font-weight: 300;
}

.portfolio-grid {
  display: grid;
  margin-top: var(--section-spacing-2);
  grid-template: 1fr / 1fr;
  grid-gap: var(--section-spacing-1);
  width: 100%;
  height: 100%;
}

.portfolio-grid-item {
  grid-row: span 2;
  grid-column: span 2;
}

.inner-container{
  max-width: 1120px;
  margin-left: auto;
  margin-right: auto;
}

.image{
  display: inline-block;
  background-color: white;
}

.tagBackground{
  width: 100%;
  background-color: white;

}

.parentColumn {
    width: 100%;
    max-width: 1200px;
    display: grid;
    /* margin-top: var(--section-spacing-2); */
    grid-template: 1fr / 1fr;
    /* grid-gap: var(--section-spacing-1); */
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
    /* margin-top: var(--section-spacing-2); */
    grid-template: 2fr 2fr / 2fr 2fr;
    grid-template-rows: 2fr 2fr;
    grid-template-columns: 2fr 2fr;
    grid-template-areas: none;
    }
    
    
</style>