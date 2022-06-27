<template>

    <div class="max-w-7xl mx-auto">
      <div class="relative justify-center z-10">
        <!-- <svg class="hidden lg:block absolute right-0 inset-y-0 h-full w-48 text-white transform translate-x-1/2" fill="currentColor" viewBox="0 0 100 100" preserveAspectRatio="none" aria-hidden="true">
          <polygon points="50,0 100,0 50,100 0,100" />
        </svg> -->

        <main class="mx-auto max-w-7xl px-4 sm:px-6  lg:px-8">
          
           
            <!-- <h1 class="text-2xl tracking-tight sm:text-1xl md:text-6xl">
            
              <span class="block white xl:inline title-white pr-8">Observe</span>
              
              <span class="block white xl:inline title-white pr-8">Question</span>

              <span class="block white xl:inline title-white pr-8">Design</span>

              <span class="block white xl:inline title-white pr-8">Build</span>
            </h1> -->

                <!-- <ul>
                     <li
                      v-for="hero in heros"
                      v-bind:key="hero.sys.id"
                      class="image mx-4 my-4"
                    >
                     <img :src="hero.heroImage.url" />
                     </li>
                </ul>     -->

            <div 
             v-for="hero in heros"
            v-bind:key="hero.sys.id">
                    <img :src="hero.heroImage.url" />
            </div>

              
            <!-- <p class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0">Anim aute id magna aliqua ad ad non deserunt sunt. Qui irure qui lorem cupidatat commodo. Elit sunt amet fugiat veniam occaecat fugiat aliqua.</p> -->
            <!-- <div class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start">
              <div class="rounded-md shadow">
                <a href="#" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 md:py-4 md:text-lg md:px-10"> Get started </a>
              </div>
              <div class="mt-3 sm:mt-0 sm:ml-3">
                <a href="#" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-indigo-700 bg-indigo-100 hover:bg-indigo-200 md:py-4 md:text-lg md:px-10"> Live demo </a>
              </div>
            </div> -->

        </main>
      </div>
    </div>
    
    <!-- <div class="lg:absolute lg:inset-y-0 lg:right-0 lg:w-1/2">
      <img class="h-56 w-full object-cover sm:h-72 md:h-96 lg:w-full lg:h-full" src="https://images.unsplash.com/photo-1551434678-e076c223a692?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2850&q=80" alt="" />
    </div> -->

</template>

<script>

export default {
  data() {
    return {
        heros: []
      };
  },

  async created() {
    this.heros = await this.getHeros();
  },

  methods: {
    getHeros: async () => {
      const query = `{
        heroCollection {
          items {
            sys {
              id
            }
          
            heroImage{
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
        console.log(response.data.heroCollection.items);
        return response.data.heroCollection.items;
      } catch (error) {
        throw new Error("Could not receive the data from Contentful!");
      }

    }
    
  }
 };
</script>

<style>

.title-white{
  font-family: 'DM Sans', sans-serif;
  font-size: 54px;
  text-align: center;
  font-weight: 300;
  color: whitesmoke;
}
 
 .bg-color-hero{
  background-color: rgb(115, 115, 115);
 }
</style>