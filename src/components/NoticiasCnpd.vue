<template>
  <!-- ======= Recent Blog Posts Section ======= -->
  <section id="noticias" class="noticias">
    <div class="container" data-aos="fade-up">
      <div class="section-bredcumbs">
        <h5>
          Onde estou?
          <router-link style="text-decoration: none" to="/">
            <b>Página Inicial</b>
          </router-link> 
          <b> > </b>
          <router-link style="text-decoration: none" to="/noticias">
            <b>Notícias</b>
          </router-link>
        </h5>
      </div>
      <div class="section-title">
        <div class="section-title">
          <h2>Todos os Eventos</h2>
        </div>
      </div>
      <div class="row">
        <div
          id="box"
          v-for="(event, index) in filteredList"
          :key="index"
          class="col-lg-3"
        >
          <div class="post-box">
            <!--:src="event.url" src="https://www.parlamento.cv/userfiles/Austelino%20FINAL(texto)(2).png"  -->
            <div class="post-img">
              <img
               :src="'http://localhost:8000/storage/capanoticia/'+ event.imagem "
                class="img-fluid"
                alt="" 
              />
            </div>
            <span class="post-date">{{ event.created_at }}</span>
            <h3 class="post-title">{{ event.titulo }}</h3>
            <router-link :to="{ name: 'eventview', params: { id: event.id } }">
              <button
                id="vermais"
                class="float-left btn btn-outline-info btn-sm"
              >
                Ler mais <IconAwe class="icon-color" icon="arrow-right" />
              </button>
            </router-link>
          </div>
        </div>
        <p></p>
        <div id="idpage">
          <button
            id="button"
            @click="prevPage"
            class="float-left btn btn-outline-info btn-sm"
          >
            <i class="fas fa-arrow-left"></i>
          </button>
          <p>&nbsp;&nbsp;</p>
          <button
            id="button"
            @click="nextPage"
            class="float-right btn btn-outline-info btn-sm"
          >
            <i class="fas fa-arrow-right"></i>
          </button>
        </div>
      </div>
    </div>
  </section>
  <!-- End Recent Blog Posts Section -->
</template>

<script>
/*eslint-disable*/
import axios from "axios";
export default {
  name: "NoticiasCnpd",
  data: () => ({
    noticias: [], //array com os itens
    currentSort: "titulo", //ordenar por titulo
    currentSortDir: "asc", // ordenar ascendente
    search: "", //search
    searchSelection: "",
    pageSize: 12, //paginacao
    currentPage: 1,
  }),

  methods: {
    sort(s) {
      if (s === this.currentSort) {
        this.currentSortDir = this.currentSortDir === "asc" ? "desc" : "asc";
      }
      this.currentSort = s;
    },
    nextPage() {
      if (this.currentPage * this.pageSize < this.noticias.length)
        this.currentPage++;
    },
    prevPage() {
      if (this.currentPage > 1) this.currentPage--;
    },

    countNumbers() {
      return this.noticias.length;
    },
  },

  computed: {
    filteredList() {
      return this.noticias
        .filter((data) => {
          let titulo = data.titulo.toLowerCase().match(this.search.toLowerCase());
          return titulo;
        })
        .filter((row, index) => {
          let start = (this.currentPage - 1) * this.pageSize;
          let end = this.currentPage * this.pageSize;
          if (index >= start && index < end) return true;
        });
    },
  },

  created() {
    axios
      .get("http://127.0.0.1:8000/api/listarNoticias")
      .then((response) => {
        this.noticias = response.data;
      });
  },
};
</script>

<style scoped>
img{
  width: auto; 
    height: auto;
}

.post-box{  
    float: left;
    margin: 3px;
    padding: 3px;
}
#box {
  margin-bottom: 10px;
}
a {
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
  background: #bd9a13;
  color: black;
  display: inline-block;
  text-transform: uppercase;
  border-radius: 50px;
}
.noticias .post-box {
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
.noticias .post-box .post-img {
  overflow: hidden;
  margin: -30px -30px 15px -30px;
  position: relative;
}
.noticias .post-box .post-img img {
  transition: 0.5s;
}
.noticias .post-box .post-date {
  font-size: 10px;
  font-weight: 600;
  color: #012970;
  display: block;
  margin-bottom: 10px;
}
.noticias .post-box .post-title {
  font-size: 15px;
  text-align: justify;
  color: #012970;
  font-weight: 700;
  margin-bottom: 18px;
  position: relative;
  transition: 0.3s;
}

.noticias .post-box:hover .post-title {
  color: #013365;
}
.noticias .post-box:hover .post-img img {
  transform: rotate(6deg) scale(1.2);
}
a {
  text-decoration: none;
  color: #493c3e;
  transition: ease-in-out 0.3s;
}

a:hover {
  color: #bd9a13;
}

#noticias {
  padding-top: 100px;
}
#idpage {
  display: flex;
  justify-content: center;
}
#button {
  color: #061536;
  border: 2px solid #061536;
  box-shadow: 1px 1px #061536;
  height: 30px;
  width: 30px;
}
#button:hover {
  box-shadow: 1px 1px 3px 3px black;
  color: #fff;
  background-color: #061536;
}
#vermais {
  color: #000;
  border: 1px solid #061536;
  background-color: #fff;
}
#vermais:hover {
  color: #fff;
  background-color: #061536;
}
</style>
