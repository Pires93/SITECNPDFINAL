<template>
  <div id="container">
    
    <div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-indicators">
      <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
      <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1" aria-label="Slide 2"></button>
      <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2" aria-label="Slide 3"></button>
      <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="3" aria-label="Slide 4"></button>
      <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="4" aria-label="Slide 5"></button>
      <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="5" aria-label="Slide 6"></button>
     </div>
    <div class="carousel-inner">
      
        <div v-for="(news, index) in (filtrarNoticias)" :key="index" class="carousel-item active">
           
          <div class="post-img">
            <img  :src="'http://localhost:8000/storage/capanoticia/'+news.imagem" class="img-fluid" alt="">
          </div>
          <div id="titlemob" class="carousel-caption d-none d-md-block"> 
            <router-link :to="{name: 'eventview',params: { id: news.id}}" style="text-decoration: none">
              <h5>  {{news.titulo}}</h5>
              <!--{{ countnews() }} -->
            </router-link> 
            <p id="textoslide">{{news.titulo}}</p> 
          </div>
        </div>
        
      <!-- MOSTRAR 3 CONSELHOS PRATICOS-->
      <div v-for="(conselho, index) in (conselhospraticos)" :key="index" class="carousel-item">
          <div class="post-img"><img  :src="conselho.url"  class="img-fluid" alt=""></div><!--src="/img/passwordforte.png" -->
          <div class="carousel-caption d-none d-md-block">
            <router-link to="/conselhos" style="text-decoration: none">
              <h5>Conselho -  {{conselho.id}}- {{conselho.title}}</h5>
            </router-link> 
            <p id="textoslide">{{conselho.title}}</p>
        </div>
      </div> 
  </div>
   
</div>
  </div>
</template>

<script>

import axios from 'axios';
export default {
  name: "BannerHome",
  data: () => ({
    photos: [],
    noticias:[], //array com os itens
    currentSort:'title', //ordenar por title
    currentSortDir:'asc',// ordenar ascendente
    search: '', //search 
    searchSelection: '',
    pageSizeconselhos: 5, //paginacao
    pageSizenews:1,
    currentPage: 1
  }),

  methods:{
    sort(s) {
      if(s === this.currentSort) {
        this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
      }
      this.currentSort = s;
    },
    nextPage:function() {
      if((this.currentPage*this.pageSize) < this.photos.length) this.currentPage++;
    },
    prevPage:function() {
      if(this.currentPage > 1) this.currentPage--;
    },

    countnews(){
      return this.noticias.length; 
    }
  },

  computed: { 

    conselhospraticos () {
      return this.photos.filter((data) => { 
        let title = data.title.toLowerCase().match(this.search.toLowerCase());  
        return title;
      }).filter((row, index) => {
        let start = (this.currentPage-1)*this.pageSizeconselhos;
        let end = this.currentPage*this.pageSizeconselhos;
        if(index >= start && index < end) return true;
      });
    },
    filtrarNoticias () {
      return this.noticias.filter((data) => { 
        let titulo = data.titulo.toLowerCase().match(this.search.toLowerCase());  
        return titulo;
      }).filter((row, index) => {
        let start = (this.currentPage-1)*this.pageSizenews;
        let end = this.currentPage*this.pageSizenews;
        if(index >= start && index < end) return true;
      });
    }
  },

  created () {
    axios.get('https://jsonplaceholder.typicode.com/photos')
      .then(response => {
        this.photos = response.data
      });
      axios.get('http://127.0.0.1:8000/api/ultimaNoticia')
      .then(response => {
        this.noticias = response.data
      })
  },

}
</script>

<style scoped>
#link{
  color: #BD9A13; 
}
 .post-img {  
}
.post-img img { 
  width: 100%;
  height: 600px;
}

@media only screen and (max-width: 600px) {
  .post-img img { 
  width: 100%;
  height: auto;
} 
}
/*
@media screen and (max-width: 767px) { 
.carousel-caption {
  display: block !important;
  font-size: 12px;
} */

/* On screens that are 600px wide or less, the background color is olive */
@media screen and (max-width: 600px) {
  h5{ 
    font-size:16px;   
    color: #fff;  
    font-weight: 500;
    display: block;
    line-height: 1.1;
}
#textoslide{
  font-size: 10px;
}

  .carousel-caption {
  display: block !important;
  font-size: 12px;
} 
}
 
@media screen and (min-width: 900px) {
  h5{
  color: #fff; 
    font-size: 50px; 
    font-weight: 1000;
    display: block;
    line-height: 1.1;
    margin-bottom: 100px; 
}
#textoslide{
  font-size: 18px;
}
}
#container {
  padding-top: 70px;
}
 
.responsive {
  width: 100%;
  height: 600px;
}
.responsiveaviso {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: auto;
  height: 600px;
}
</style>