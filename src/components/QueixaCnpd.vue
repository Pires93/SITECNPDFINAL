<template>
  <!-- ======= queixa Section ======= -->
  <section id="queixa" class="queixa">
    <div class="container">
      <div class="section-title">
        <h2>FORMULÁRIO DE APRESENTAÇÃO DE QUEIXAS/RECLAMAÇÕES</h2>
      </div>
      <div class="col-md-12"  id="divg">
        <Form @submit="onSubmit">  
          <div class="row">
            <div class="col-md-6">
              <p class="pleft"> Dados do queixoso:</p>
               
              <div class="col-md-12" id="divloco"> 
               <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="name"
                  id="name"
                  placeholder="Seu Nome"
                 />
                <ErrorMessage class="errorMessage" name="name" /> 
              </div>
              <div class="col-md-12" id="divloco">
              <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="address"
                  id="address"
                  placeholder="Sua morada ..."
                 />
                <ErrorMessage class="errorMessage" name="address" /> 
              </div>
              <div class="col-md-12" id="divloco"> 
               <Field
                  :rules="validateNumber"
                  type="text"
                  class="form-control"
                  name="phone"
                  id="phone"
                  placeholder="Nº de telefone Ex: 5900000"
                 />
                <ErrorMessage class="errorMessage" name="phone" /> 
              </div>
              <div class="col-md-12"  id="divloco"> 
                <Field
                  :rules="validateEmail"
                  type="email"
                  class="form-control"
                  name="email"
                  id="email"
                  placeholder="Entre seu email Ex: cnpd@cnpd.cv"
                  />
                <ErrorMessage class="errorMessage" name="email" /> 
              </div>
            </div>

            <div class="col-lg-6" id="divloco">
              <p class="pleft"> Dados do denunciado:</p>
              <div class="col-md-12"> 
              <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="entidade"
                  id="entidade"
                  placeholder="Queixa contra a Pessoa/Empresa/Entidade ... Ex: Empresa XPTO"
                     />
                <ErrorMessage class="errorMessage" name="entidade" /> 
              </div>
              <div class="col-md-12" id="divloco">
                <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="entidadeaAdress"
                  id="entidadeaAdress"
                  placeholder="Morada da Pessoa/Empresa/Entidade... Ex: Palmarejo"
                    />
                <ErrorMessage class="errorMessage" name="entidadeaAdress" /> 
              </div>
              <div class="col-md-12" id="divloco"> 
                <Field
                  :rules="validateNumber"
                  type="text"
                  class="form-control"
                  name="entidadePhone"
                  id="entidadePhone"
                  placeholder="Nº de telefone da Pessoa/Empresa/Entidade... Ex: 5900000"
                />
                <ErrorMessage class="errorMessage" name="entidadePhone" /> 
              </div>
              <div class="col-md-12" id="divloco">
                <Field
                  :rules="validateEmail"
                  type="email"
                  class="form-control"
                  name="entidadeEmail"
                  id="entidadeEmail"
                  placeholder="Entre o email da Pessoa/Empresa/Entidade...  Ex: xpto@xpto.cv"
                  />
                <ErrorMessage class="errorMessage" name="entidadeEmail" /> 
              </div>
            </div>
            
            <p class="pleft"> Obejeto da sua queixa:</p>
            <div class="col-md-12" id="divloco"> 
              <Field
                :rules="validateText"
                type="text"
                class="form-control"
                name="subject"
                id="subject"
                placeholder="Qual o assunto da sua queixa"
              />
              <ErrorMessage class="errorMessage" name="subject" /> 
            </div>
            <div class="col-md-12" id="divloco"> 
              <Field
                :rules="validateText"
                type="text"
                as="textarea"
                class="form-control"
                name="message"
                id="message" 
                placeholder="Descreva a sua queixa em detalhes ..."
              />
              <ErrorMessage class="errorMessage" name="message" />  
            </div>
          </div>
          <br>
          <div class="col-md-12" id="divsave">
          <button
            @click="submitForm"
            id="buttonsave"
            class="btn btn-primary"
            type="submit"
          >
          <IconAwe class="icon-color" icon="paper-plane"
                    /> Submeter Dados
          </button>
        </div> 
        </Form>
      </div>
    </div>
  </section>
  <!-- End queixa Section -->
</template>

<script> 
import { Form, Field, ErrorMessage } from "vee-validate";

export default { 
  components: {
    Form,
    Field,
    ErrorMessage, 
  }, 

  methods: {
    onSubmit(values) {
      console.log(values, null, 2);
      console.log("Clckado");
    },
    validateText(value) {
      // if the field is empty
      if (!value) {
        return "Campo obrigatório!";
      }
      return true;
    },
 
    validateNumber(value) {
      // if the field is empty
      if (!value) {
        return "Campo obrigatório!";
      }
      // if the field is not a valid number
      const regex = /[0-9]/;
      if (!regex.test(value)) {
        return "Carater inválido, precisa ser um número!";
      }

      return true;
    },
    validateEmail(value) {
      // if the field is empty
      if (!value) {
        return "Campo obrigatório!";
      }
      // if the field is not a valid email
      const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
      if (!regex.test(value)) {
        return "Email inválido, precisa ser nesse formato: cnpd@example.cv";
      }
      // All is good
      return true;
    }
  }
  
};
</script>

<style scoped>
/*--------------------------------------------------------------
# queixa
--------------------------------------------------------------*/
#divg {
  font-family: "Times New Roman", Times, serif;
  border: 1px solid #061536;
  padding: 10px;
  border-radius: 10px;
}
#buttonsave {
  background-color: #061536;
}
#divsave {
  margin-top: 10px;
  text-align: center;
}
button#buttonsave:hover,
button#buttonsave:focus {
  background-color: #061536;
  outline: none !important;
  border-color: #061536;
  color: #bd9a13;
  box-shadow: 0 0 10px #061536;
}
#divloco {
  margin-top: 10px;
}
.pleft{
    text-align: left;  
    font-weight: bold
}
#queixa {
  padding-top: 60px;
}
#framemaps {
  border-radius: 1%;
  width: 100%;
  height: 400px;
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
.section-title h3 {
  margin: 15px 0 0 0;
  font-size: 32px;
  font-weight: 700;
}
.section-title h3 span {
  color: #000;
}
.section-title p {
  margin: 15px auto 0 auto;
  font-weight: 600;
}
@media (min-width: 1024px) {
  .section-title p {
    width: 50%;
  }
}
.queixa .info {
  width: 100%;
  background: #fff;
}
.queixa .info i {
  font-size: 20px;
  color: #030b1c;
  float: left;
  width: 32px;
  height: 32px;
  background: #bd9a13;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50px;
  transition: all 0.3s ease-in-out;
}
.queixa .info h4 {
  padding: 0 0 0 60px;
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 5px;
  color: #493c3e;
}
.queixa .info p {
  padding: 0 0 0 60px;
  margin-bottom: 0;
  font-size: 14px;
  color: #000;
}
.queixa .info .email,
.queixa .info .phone {
  margin-top: 40px;
}
.queixa .info .email:hover i,
.queixa .info .address:hover i,
.queixa .info .phone:hover i {
  color: #fff;
}
.queixa .php-email-form {
  width: 100%;
  background: #fff;
}
.queixa .php-email-form .form-group {
  padding-bottom: 8px;
}
.queixa .php-email-form .error-message {
  display: none;
  color: #fff;
  background: #ed3c0d;
  text-align: left;
  padding: 15px;
  font-weight: 600;
}
.queixa .php-email-form .error-message br + br {
  margin-top: 25px;
}
.queixa .php-email-form .sent-message {
  display: none;
  color: #fff;
  background: #18d26e;
  text-align: center;
  padding: 15px;
  font-weight: 600;
}
.queixa .php-email-form .loading {
  display: none;
  background: #fff;
  text-align: center;
  padding: 15px;
}
.queixa .php-email-form .loading:before {
  content: "";
  display: inline-block;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  margin: 0 10px -6px 0;
  border: 3px solid #18d26e;
  border-top-color: #eee;
  -webkit-animation: animate-loading 1s linear infinite;
  animation: animate-loading 1s linear infinite;
}
.queixa .php-email-form input,
.queixa .php-email-form textarea {
  border-radius: 0;
  box-shadow: none;
  font-size: 14px;
}
.queixa .php-email-form input:focus,
.queixa .php-email-form textarea:focus {
  border-color: #030b1c;
}
.queixa .php-email-form input {
  height: 44px;
}
.queixa .php-email-form textarea {
  padding: 10px 12px;
}
.queixa .php-email-form button[type="submit"] {
  background: #bd9a13;
  border: 0;
  padding: 10px 28px;
  color: #000;
  font-weight: bold;
  transition: 0.4s;
  border-radius: 50px;
}
.queixa .php-email-form button[type="submit"]:hover {
  background: #bd9a13;
}
@-webkit-keyframes animate-loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes animate-loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.icon-color {
  font-size: 14px;
}
</style>
