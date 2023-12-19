<template>
<br> <br> <!--filtering it so that you get it by genres-->
<div class="wrapper" v-if="products" >
  <div class="row-wrapper">
    <div id="select-wrapper"> <!--ensuring that all genres will be displayed in the drop down buttom-->
      <select name="mangaGenre" id="mangaGenre" v-model="genre">
      <option v-for="genre in filterByGenre" :key="genre" :value="genre">
      {{ genre }} <!--claiming it-->
      </option>
      </select>
    </div>
  </div>

  <!-- my search bar-->
<div class="search-wrapper">
  <input type="text" placeholder="Search for a manga... " v-model ="searchNames" @keyup="retrieveProduct">
</div>

  <div class="row-wrapper" v-if="renderProducts">
            <div class="prodCard" v-for="product in products" :key="product.id">
                <div class="card-header">
                    <h3>{{ product.mangaName }}</h3> 
                    <p>{{ manga.genre }}</p>
                </div>
                <div class="card-body">
                    <img :src="product.image" :alt="product.mangaName" loading="lazy">
                    <p>R{{ product.amount }},00</p>
                </div> 
                <div class="card-footer">
                    <a href="#" type="button">View Details</a>
                </div>
            </div>
        </div>  
    </div>
    <div v-else>
      <h3>Out of manga at the moment,shall be in stock soon!</h3>
    </div>
</template>

<script>
export default {
  name: 'ProductComp',
data() {
  return {
    products: [
      {
        id: 1,
        mangaName: 'Death Note',
        genre: 'Psychological',
        amount: 350,
        image: 'https://i.postimg.cc/157HyrtV/Death-Note-Manga.jpg',
      },
      {
        id: 2,
        mangaName: 'One Punch Man',
        genre: 'Action',
        amount: 350,
        image: 'https://i.postimg.cc/bvHv8LTQ/one-punch-man-vol-1-yusuke-murata-28400120266867-86936.jpg',
      },
      {
        id: 3,
        mangaName: 'Nichijou',
        genre: 'Slice of Life',
        amount: 280,
        image: 'https://i.postimg.cc/LX0bGKrh/Nichijou.jpg'
      },
    ],
    selectedGenre: 'All Genres', //forgotten to include all 
    searchNames: ''
  }
},

computed: {
  filterByGenre() {
    return['All Products'].concat(Array.from(new Set(this.products.map(item => item.genre))))
  },
  renderProducts() {
    return this.selectedGenre.toLowerCase() != "al products" ? this.products.filter(item =>item.genre.toLowerCase().includes(this.selectedGenre.toLowerCase())) : this.searchNames.toLowerCase() ? this.products.filter(item =>item.genre.toLowerCse().includes(this.searchNames.toLowerCase())) : this.products //making it so that we are able to searcg for the items by name and by genre but we have to place it in lowercase for better computer reabbility. 
  },
}
}
</script>

<style scoped>
.row-wrapper {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
</style>


