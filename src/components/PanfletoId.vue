<template>
  <!-- ======= eventcoes Section ======= -->
  <section id="panfletid" class="panfletid">
    <div class="container">
      <div class="section-bredcumbs">
        <h5>
          Onde estou?
          <router-link style="text-decoration: none" to="/">
            <b>Página Inicial</b>
          </router-link>
          <b> > </b>
          <router-link style="text-decoration: none" to="#">
            <b>Publicações</b>
          </router-link>
          <b> > </b>
          <router-link style="text-decoration: none" to="/panfletos">
            <b>Panfletos Publicados</b>
          </router-link>
          <b> > </b>
          <router-link style="text-decoration: none" to="#">
            <b v-if="listaDados">Panfleto Nº.{{ listaDados.num_doc }} - {{ listaDados.titulo }}</b>
          </router-link>
        </h5>
      </div>
      <div v-if="listaDados">
        <div class="section-title">
          <h2>{{ listaDados.titulo }}</h2> 
        </div>
        <div class="row content">
          <a class="downloadpdf" target="_blank" :href="'http://localhost:8000/storage/publicacoesPdf/'+ listaDados.anexo " download>
            <img src="/img/downloadpdf.png"  style="width: 140px" />
          </a>
          <!--FLIPBOOK-->

          <iframe
            id="frame"
            :src="listaDados.link"
            width="100%"
            height="600"
            style="border: none"
            allowFullScreen
          >
          </iframe>

          <!--FLIPBOOK-->
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "PanfletoId",
  props: ["id"],

  data: function () {
    return {
      listaDados: null,
    };
  },

  mounted() {
    fetch("http://127.0.0.1:8000/api/panfleto/" + this.$route.params.id)
      .then((response) => response.json())
      .then((data) => (this.listaDados = data))
      .catch((err) => console.log(err.message));
  },
};
</script>

<style scoped>
#frame {
  border: 2px solid red;
  padding: 10px;
  border-radius: 25px;
}
.flipbook {
  width: 90vw;
  height: 90vh;
  background-color: red;
}
.panfletid {
  padding-top: 100px;
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
  color: #000;
  display: inline-block;
  text-transform: uppercase;
  border-radius: 50px;
}
@media (min-width: 1024px) {
  .section-title p {
    width: 50%;
  }
}

.post-img {
  padding-top: 20px;
  overflow: hidden;
  margin: -30px -30px 15px -30px;
  position: relative;
  height: 500px;
}

img {
  border-radius: 10px;
}
#descricao {
  text-align: justify;
  padding-left: 50px;
}
.date {
  font-size: 14px;
  color: #013365;
}
</style>
