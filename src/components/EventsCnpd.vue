<template>
<!-- ======= Recent Blog Posts Section ======= -->
    <section id="recent-blog-posts" class="recent-blog-posts">

      <div class="container" data-aos="fade-up"> 

        <div class="section-title"> 
          <div class="section-title">
               <h2>Eventos recentes </h2>  
           </div>
        </div> 
        <div class="row"> 
          <div id="box" v-for="(event, index) in (filteredList)" :key="index" class="col-lg-4"> 
            <div class="post-box"> <!--:src="event.url" -->
              <div class="post-img">
                <img  :src="'http://localhost:8000/storage/capanoticia/'+event.imagem" class="img-fluid" alt="">
              </div>
              <span class="post-date">{{event.created_at}}</span>
              <h3 class="post-title">{{event.titulo}}</h3>
              <router-link :to="{name: 'eventview',params: { id: event.id}}">
               <span>Ler mais </span> <IconAwe class="icon-color" icon="arrow-right" />
              </router-link>  
            </div>
          </div> 

        </div>

      </div>

    </section><!-- End Recent Blog Posts Section -->
   
   
</template>

<script>
/*eslint-disable*/
import axios from 'axios';
export default {
    name:"EventsCnpd",
    data: () => ({
    noticias: [], //array com os itens
    currentSort:'titulo', //ordenar por title
    currentSortDir:'asc',// ordenar ascendente
    search: '', //search 
    searchSelection: '',
    pageSize: 3, //paginacao
    currentPage: 1
  }),

  methods:{
    sort(s) {
      if(s === this.currentSort) {
        this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
      }
      this.currentSort = s;
    },
    nextPage() {
      if((this.currentPage*this.pageSize) < this.noticias.length) this.currentPage++;
    },
    prevPage() {
      if(this.currentPage > 1) this.currentPage--;
    },

    countNumbers(){
      return this.noticias.length; 
    }
  },

  computed: { 

    filteredList () {
      return this.noticias.filter((data) => { 
        let titulo = data.titulo.toLowerCase().match(this.search.toLowerCase());  
        return titulo;
      }).filter((row, index) => {
        let start = (this.currentPage-1)*this.pageSize;
        let end = this.currentPage*this.pageSize;
        if(index >= start && index < end) return true;
      });
    }
  },

  created () {
    axios.get('http://127.0.0.1:8000/api/ultimosEventos')
      .then(response => {
        this.noticias = response.data
      })
  },

}
</script> 

<style scoped>
a{
  text-decoration: none;
}
.section-title {
  text-align: center;
  padding-bottom: 30px;
}
.section-title h2 {
  font-size: 13px;
  letter-spacing: 1px;
  font-weight: 700;
  padding: 8px 20px;
  line-height: 1;
  margin: 0;
  margin-top: 40px;
  background: #BD9A13;
  color: black;
  display: inline-block;
  text-transform: uppercase;
  border-radius: 50px;
}
.recent-blog-posts .post-box {
  box-shadow: 0px 0 30px rgba(1, 41, 112, 0.08);
  transition: 0.3s;
  height: 100%;
  overflow: hidden;
  padding: 30px;
  border-radius: 8px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.recent-blog-posts .post-box .post-img {
  overflow: hidden;
  margin: -30px -30px 15px -30px;
  position: relative;
}
.recent-blog-posts .post-box .post-img img {
  transition: 0.5s;
}
.recent-blog-posts .post-box .post-date {
  font-size: 12px;
  font-weight: 600;
  color: #012970;
  display: block;
  margin-bottom: 10px;
}
.recent-blog-posts .post-box .post-title {
  font-size: 16px;
  text-align: justify;
  color: #012970;
  font-weight: 700;
  margin-bottom: 18px;
  position: relative;
  transition: 0.3s;
}
 
 
.recent-blog-posts .post-box:hover .post-title {
  color: #013365;
}
.recent-blog-posts .post-box:hover .post-img img {
  transform: rotate(6deg) scale(1.2);
}
a{
  text-decoration: none;
  color: #493c3e;
  transition: ease-in-out 0.3s;
}

a:hover{
    color: #BD9A13;
}
</style>