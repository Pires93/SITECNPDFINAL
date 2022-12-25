<template>
  <section id="videos" class="videos">

<div class="container" data-aos="fade-up"> 

<div class="section-title"> 
  <div class="section-title">
       <h2>APIS CONSUMIDOS VOU CONSUMIR ALGUM API AQUI</h2>  
   </div>
</div> 
<div class="row">  
  {{ info }}
   
</div>

</div>

</section><!-- End Recent Blog Posts Section -->


</template>

<script>  
 


export default {
  name:"TesteApi",
  data: () => ({ 
}),
 
}

</script>

<style scoped>
#idsearch{
width: 40%;
height: 30px;
text-align: center;
box-shadow: 1px 1px  #061536;
}

#idpage{ 
display: flex;
justify-content: space-between;
}
#button{
 
color: #061536;
border: 2px solid #061536;
box-shadow: 1px 1px #061536;
height: 30px;
width: 30px; 
}
#button:hover{
box-shadow: 1px 1px  3px 3px black;
color: #fff;
background-color: #061536;
}
#box{ 
margin-bottom: 15px;
}
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
  background: #BD9A13;
  color: black;
  display: inline-block;
  text-transform: uppercase;
  border-radius: 50px;
}
.videos .post-box {
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
.videos .post-box .post-img {
  overflow: hidden;
  margin: -30px -30px 15px -30px;
  position: relative;
}
.videos .post-box .post-img img {
  transition: 0.5s;
}
.videos .post-box .post-date {
  font-size: 10px;
  font-weight: 600;
  color: #012970;
  display: block;
  margin-bottom: 10px;
}
.videos .post-box .post-title {
  font-size: 15px;
  text-align: justify;
  color: #012970;
  font-weight: 700;
  margin-bottom: 18px;
  position: relative;
  transition: 0.3s;
}
 
 
.videos .post-box:hover .post-title {
  color: #013365;
}
.videos .post-box:hover .post-img video {
  box-shadow: 1px 1px  3px 5px black; 
transition: all 0.2s ease-in-out;
}
a{
  text-decoration: none;
  color: #493c3e;
  transition: ease-in-out 0.3s;
}

a:hover{
    color: #BD9A13;
}

#videos {  
  padding-top: 120px; 
} 
#idpage{ 
 
  display: flex;
  justify-content: center;
} 
.post-img :hover{
cursor: pointer;

}
video{
object-fit: cover;
}
</style>