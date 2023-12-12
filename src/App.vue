<template>
  <div>
    <h1 class="heading">List of Manga</h1>
  </div> 
<br> <br>
<div class="wrapper" >
  <form @submit ="registerAnswer" id="thisForm">
    <label for="manga">Genres:</label>
    <select  v-model="genreSelected" id="genre">
      <option disabled value="">Please select one</option>
      <option>Action</option>
      <option>Psychological</option>
      <option>Slice of Life</option>

      <option v-for="genre in uniqueGenres" :key="genre">{{ genre }}</option>
    </select>
    <br><br>
    <input type="submit" value="Submit">
  </form>
  <div>
    <p id="pAnswer">{{ inpValSubmitted }}</p>
  </div>
</div>

<div class="wrapper">
  <input type="text" v-model ="searchName" @input="onSearch"  placeholder="Search for a manga...">
</div>

  <div class="wrapper">
        <div class="row" v-if="products.length"> 
            <div class="prodCard" v-for="manga in products" :key="manga.id">
                <div class="card-header">
                    <h3>{{ manga.mangaName }}</h3> 
                    <p>{{ manga.genre }}</p>
                </div>
                <div class="card-body">
                    <img :src="manga.image" :alt="manga.mangaName" loading="lazy">
                    <p>R{{ manga.amount }},00</p>
                </div> 
                <div class="card-footer">
                    <a href="#" type="button">View Details</a>
                </div>
            </div>
          
        </div>  
    </div>
</template>

<script>

export default {
  name: 'MangaComp',
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
      genre: '',
      inpValSubmitted: ''
    }
  },
  methods: {
    registerAnswer() {
      if(this.genreSelected) {
        this.inpValSubmitted = this.genreSelected;
      }
    },
  },
  computed : {
    uniqueGenres() {
      return [...new Set(this.products.map(manga => manga.genre))];
  }
},
</script>

<style>
#app {
  font-family: cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:white;
  background-color: black;
  margin-top: 60px;
}

.heading {
  text-align: center;
  color: yellow;
}

#thisForm {
  color: yellow;
  font-family: cursive;
}
</style>
