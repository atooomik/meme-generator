<template>
  <div class="bg-gray-900 w-full h-screen overflow-scroll">
    <div class="max-w-screen-2xl w-full mx-auto text-center">
      <div class="bg-gray-800 my-4 py-4 text-gray-500 rounded-lg">
        <p>Memeteca</p>
      </div>
      <div class="bg-gray-800 text-gray-500 p-4 text-left">
        <p class="py-2 text-gray-500">Busca por nombre</p>
        <input
          type="text"
          v-model="querySearch"
          aria-label="Busqueda por nombre o termino"
          class="bg-gray-700 border border-gray-700 rounded-lg p-2"
        />

        <button
          @click="filterMemes"
          class="bg-gray-700 rounded-lg px-2 py-2 ml-4 text-gray-500"
        >
          Buscar
        </button>
        <button
          @click="cleanSearch"
          class="bg-gray-700 rounded-lg px-2 py-2 text-gray-500 ml-4"
        >
          Restablecer
        </button>
      </div>
      <div class="grid grid-cols-3 grid-rows-6 p-2 gap-6 pt-6">
        <sample-card
          v-for="(meme, index) in selectedData"
          :key="index"
          :raw-data="meme"
        ></sample-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data: () => {
    return {
      originalData: [],
      selectedData: [],
      querySearch: '',
    }
  },
  mounted() {
    this.fetchMemes()
  },
  methods: {
    storeData(data) {
      this.originalData = data
      this.selectedData = this.originalData
    },
    fetchMemes() {
      this.$axios.$get('https://api.imgflip.com/get_memes').then((response) => {
        this.storeData(response.data.memes)
      })
    },
    filterMemes() {
      const word = this.querySearch
      const filterResults = []
      this.selectedData.forEach((element) => {
        if (element.name.includes(word)) {
          filterResults.push(element)
        }
      })
      this.selectedData = filterResults
    },
    cleanSearch() {
      this.selectedData = this.originalData
      this.querySearch = ''
    },
  },
}
</script>
