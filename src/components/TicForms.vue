<template>
  <section id="Interconexao" class="Interconexao">
    <div class="container">
      <div class="section-bredcumbs">
        <h5>
          Onde estou?
          <router-link style="text-decoration: none" to="/">
            <b>Página Inicial</b>
          </router-link>
          <b> > </b>
          <router-link style="text-decoration: none" to="/formularios">
            <b>Formulários</b>
          </router-link>
          <b> > </b>
          <router-link style="text-decoration: none" to="/formstic">
            <b>Formulário de TIC</b>
          </router-link>
        </h5>
      </div>
      <Form @submit="onSubmit">
        <!-- FORMS Interconexao-->
        <div class="section-title">
          <h2>
            Notificação do controlo de utilização de tefone/correio electtrónico
            e internet
          </h2>
        </div>
        <div class="col-md-12"></div>
        
     <div class="col-md-12" id="divg">
        <div class="container">
          <div class="row">
            <div class="col-md-2">
              <label id="labelleft" for="TipoNot" class="form-label"
                >Tipo Notificação</label
              >
            </div>
            <div class="col-md-10">
              <Field
                  name="tipoNotificacao"
                  as="select"
                  class="form-select"
                  v-model="tipoNotificacao"
                  :rules="validateRadio"
                >
                  <option value="">- selecione o tipo de Notificação -</option>
                  <option
                    v-for="tipoNotificacao in tipoNotificacoes"
                    :key="tipoNotificacao.value"
                    :value="tipoNotificacao.value"
                  >
                    {{ tipoNotificacao.value }}
                  </option>
                </Field>
                <ErrorMessage class="errorMessage" name="tipoNotificacao" />
            </div>
          </div>
        </div>
      </div>

        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                1. Responsável pelo Tratamento
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-4"></div>
              <div class="col-md-2" id="alignCenter">
                <Field
                  :rules="validateRadio"
                  type="radio"
                  id="tipoPessoa"
                  name="tipoPessoa"
                  value="Pessoa Singular"
                  v-model="tipoPessoa"
                />
                <label for="Pessoa Singular"> Pessoa Singular</label>
              </div>
              <div class="col-md-2" id="alignCenter">
                <Field
                  :rules="validateRadio"
                  type="radio"
                  id="tipoPessoa"
                  name="tipoPessoa"
                  value="Pessoa Coletiva"
                  v-model="tipoPessoa"
                />
                <label for="Pessoa Coletiva"> Pessoa Coletiva</label>
              </div>
              <div class="col-md-4"></div>
              <div class="col-md-12" id="alignCenter">
                <ErrorMessage class="errorMessage" name="tipoPessoa" />
              </div>

              <div class="col-md-12">
                <Field
                  name="nomedenominacao"
                  type="text"
                  class="form-control"
                  id="nomedenominacao"
                  alt="Nome Denominação: Refere-se à designação oficial de uma instituição pública ou privada"
                  placeholder=" Nome/Denominação"
                  :rules="validateText"
                />
                <ErrorMessage class="errorMessage" name="nomedenominacao" />
              </div>
              <div class="col-md-12">
                <input
                  type="text"
                  class="form-control"
                  id="nomecomercial"
                 
                  placeholder=" Nome/Comercial"
                />
              </div>
              <div class="col">
                <Field
                  name="atividadeDesenvolvida"
                  as="select"
                  class="form-select"
                  v-model="atividadeDesenvolvida"
                  :rules="validateRadio"
                >
                  <option value="">- Selecione a atividade desenvolvida -</option>
                  <option
                    v-for="atividadeDesenvolvida in atividadesDesenvolvidas"
                    :key="atividadeDesenvolvida.value"
                    :value="atividadeDesenvolvida.value"
                  >
                    {{ atividadeDesenvolvida.value }}
                  </option>
                </Field>
                <ErrorMessage
                  class="errorMessage"
                  name="atividadeDesenvolvida"
                />
              </div>
              <div class="col">
                <Field
                  name="nif"
                  type="text"
                  class="form-control"
                  id="nif"
                  alt="NIF"
                  placeholder="Número de NIF"
                  :rules="validateNumber"
                />
                <ErrorMessage class="errorMessage" name="nif" />
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <input
                      type="text"
                      class="form-control"
                      id="rua"
                      alt="RUA"
                      placeholder="Entre o nome da Rua"
                    />
                  </div>
                  <div class="col">
                    <Field
                      name="local"
                      type="text"
                      class="form-control"
                      id="local"
                      alt="Local"
                      placeholder="Cidade/Vila/Lugar/Zona"
                      :rules="validateText"
                    />
                  <ErrorMessage class="errorMessage" name="local" />
                  </div>
                </div>
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <Field
                      as="select"
                      class="form-select"
                      v-model="ilhaResp"
                      name="ilhaResp"
                      id="ilhaResp"
                      for="ilhaResp"
                      placeholder="- Seleciona uma ilha-"
                      :rules="validateRadio"
                    >
                      <option value="">- selecione uma ilha -</option>
                      <option
                        v-for="option in ilhas"
                        :key="option.value"
                        :value="option.value"
                      >
                        {{ option.label }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="ilhaResp" />
                  </div>
                  <div class="col">
                    <Field
                      as="select"
                      class="form-select"
                      v-model="concelhoResp"
                      name="concelhoResp"
                      id="concelhoResp"
                      for="concelhoResp"
                      placeholder="- Seleciona um concelho -"
                      :rules="validateRadio"

                    >
                      <option value="">- selecione um concelho -</option>
                      <option
                        v-for="option in concelhos[ilhaResp]"
                        :key="option.value"
                        :value="option.value"
                      >
                        {{ option.label }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="concelhoResp" />
                  </div>
                </div>
              </div>
              <div class="col-md-12" id="divloco">
                <div class="row">
                  <div class="col">
                    <input
                      type="text"
                      class="form-control"
                      id="caixapostal"
                      alt="Caixa Postal"
                      placeholder="Entre o número da Caixa Postal"
                    />
                  </div>
                  <div class="col">
                    <Field
                      name="telefone"
                      type="number"
                      class="form-control"
                      id="telefone"
                      alt="Telefone/Telemovel"
                      placeholder="Contato: Telefone/Telemovel"
                      :rules="validateNumber"
                    />
                    <ErrorMessage class="errorMessage" name="telefone" />
                  </div>
                </div>
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <Field
                      name="email"
                      type="email"
                      class="form-control"
                      id="email"
                      placeholder="Entre o seu email: example@cnpd.cv"
                      :rules="validateEmail"
                    />
                    <ErrorMessage class="errorMessage" name="email" />
                  </div>
                  <div class="col-md-6">
                    <div class="col">
                      <Field
                        :rules="validateRadio"
                        type="radio"
                        id="paisResp"
                        name="paisResp"
                        value="Cabo Verde"
                        v-model="paisResp"
                      />
                      <label for="Cabo Verde"> Cabo Verde </label>
                    </div>
                    <div class="col">
                      <Field
                        :rules="validateRadio"
                        type="radio"
                        id="paisResp"
                        name="paisResp"
                        value=" Fora do Território Nacional"
                        v-model="paisResp"
                      />
                      <label for=" Fora do Território Nacional">  Fora do Território Nacional</label>
                    </div> 
                    <div class="col-md-6">
                      <ErrorMessage class="errorMessage" name="paisResp" />
                    </div> 
                  </div>
                </div>
              </div>
              <div class="col-md-12">
                <Field
                  name="representante"
                  type="text"
                  class="form-control"
                  id="representante"
                   placeholder="Representante"
                  :rules="validateText"
                />
                <ErrorMessage class="errorMessage" name="representante" />
              </div>
              <div class="col-md-12">
                <input
                  type="text"
                  class="form-control"
                  name="nomecomercialRI"
                  id="nomecomercialRI" 
                  placeholder=" Nome/Comercial"
                />
              </div>
              <div class="col-md-12">
                <input
                  type="text"
                  class="form-control"
                  id="ruaRI" 
                  name="ruaRI"
                  placeholder=" Rua"
                />
              </div>
              <div class="col-md-12">
                <input
                  type="text"
                  class="form-control"
                  id="caixaPostalRI" 
                  name="caixaPostalRI"
                  placeholder=" Caixa Postal"
                />
              </div>
              <div class="col-md-12">
                <Field
                  name="localRepresentante"
                  type="text"
                  class="form-control"
                  id="localRepresentante"  
                  placeholder=" Cidade/Vila/Lugar/Zona"
                  :rules="validateText"
                />
                <ErrorMessage class="errorMessage" name="localRepresentante" />
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <Field
                      as="select"
                      class="form-select"
                      v-model="ilhaMorRep"
                      name="ilhaMorRep"
                      id="ilhaMorRep"
                      for="ilhaMorRep"
                      placeholder="- Seleciona uma ilha-"
                      :rules="validateRadio"
                    >
                      <option value="">- selecione uma ilha -</option>
                      <option
                        v-for="option in ilhas"
                        :key="option.value"
                        :value="option.value"
                      >
                        {{ option.label }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="ilhaMorRep" />
                  </div>
                  <div class="col">
                    <Field
                      as="select"
                      class="form-select"
                      v-model="concelhoMorRep"
                      name="concelhoMorRep"
                      id="concelhoMorRep"
                      for="concelhoMorRep"
                      placeholder="- Seleciona um concelho -"
                      :rules="validateRadio"
                    >
                      <option value="">- selecione um concelho -</option>
                      <option
                        v-for="option in concelhos[ilhaMorRep]"
                        :key="option.value"
                        :value="option.value"
                      >
                        {{ option.label }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="concelhoMorRep" />
                  </div>
                </div>
              </div>
              <div class="col-md-12" id="divloco">
                <Field
                  type="text"
                  class="form-control"
                  name="nomePessoaContato"
                  id="nomePessoaContato" 
                  placeholder=" Nome da pessoa do contato"
                  :rules="validateText"
                />
                <ErrorMessage class="errorMessage" name="nomePessoaContato" />
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <Field
                      name="emailRepresentante"
                      type="email"
                      class="form-control"
                      id="emailRepresentante" 
                      placeholder="Entre o seu email: example@cnpd.cv"
                      :rules="validateEmail"
                    />
                    <ErrorMessage class="errorMessage" name="emailRepresentante" />
                  </div>
                  <div class="col">
                    <Field
                      name="telefoneRepresentante"
                      type="number"
                      class="form-control"
                      id="telefoneRepresentante" 
                      placeholder="Contato: Telefone/Telemovel"
                      :rules="validateNumber"
                    />
                    <ErrorMessage class="errorMessage" name="telefoneRepresentante" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

       <!---- ----------------- Processamento da informação--------------------------------------------------------------------->
       <div class="col" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                Processamento da informação
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col">
                <label class="form-check-label">
                  Existe um Serviço Externo encarregado do processamento?
                </label>
                <buttom
                  @click="changeServico"
                  type="button"
                  class="btn btn-outline-primary"
                  name="morada"
                  id="moradasimbotton"
                >
                  {{ checkServico ? "Não" : "Sim" }}
                </buttom>
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12"  v-if="checkServico">
                <div class="col-md-12">
                  <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="entidadeProcessInfo"
                  id="entidadeProcessInfo"
                  placeholder=" Qual a Entidade Encarregue pelo proccessamento das imagens"
                />
                <ErrorMessage class="errorMessage" name="entidadeProcessInfo" /> 
                </div>
                <div class="col-md-12">
                  <input
                  
                  type="text"
                  class="form-control"
                  name="ruaProcessInfo"
                  id="ruaProcessInfo"
                  placeholder=" Rua"
                />
                 
                </div>
                <div class="col-md-12">
                  <input
                 
                  type="text"
                  class="form-control"
                  name="caixaPostalProcessInfo"
                  id="caixaPostalProcessInfo"
                    placeholder=" Caixa Postal"
                />
                 
                </div>
                <div class="col-md-12">
                  <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="lugarProcessInfo"
                  id="lugarProcessInfo"
                    placeholder="Cidade/Vila/Lugar/Zona da Entidade"
                />
                <ErrorMessage class="errorMessage" name="lugarProcessInfo" />   
                </div>

                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                      as="select"
                      class="form-select"
                      v-model="ilhaServExt"
                      name="ilhaServExt"
                      id="ilhaServExt"
                      for="ilhaServExt"
                      :rules="validateRadio"
                        placeholder="- Seleciona uma ilha-"
                    >
                      <option value="">- selecione uma ilha -</option>
                      <option
                        v-for="ilha in ilhas"
                        :key="ilha.value"
                        :value="ilha.value"
                      >
                        {{ ilha.value }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="ilhaServExt" /> 
                    </div>
                    <div class="col">
                      <Field
                      as="select"
                      class="form-select"
                      v-model="concelhoServExt"
                      name="concelhoServExt"
                      id="concelhoServExt"
                      for="concelhoServExt"
                      :rules="validateRadio"
                    >
                      <option value="">- selecione um concelho -</option>
                      <option
                        v-for="concelho in concelhos[ilhaServExt]"
                        :key="concelho.value"
                        :value="concelho.value"
                      >
                        {{ concelho.value }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="concelhoServExt" />
                        </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!--------------------------------------FINALIDADE DO TRATAMENTO----------------------------------------------------->

        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="divloco">
                <div class="col-md-12" id="separacao">
                  2. Finalidade do tratamento
                </div>
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col">
                <Multiselect
                  v-model="value"
                  name="finalidadetra"
                  id="finalidadetra"
                  placeholder="- Indique a(s) finalidade(s) do tratamento-"
                  mode="tags"
                  :close-on-select="false"
                  :searchable="true"
                  :create-option="true"
                  :options="finalidadeTratamento"
                />
              </div>
            </div>
          </div>
        </div>
    <!---- ----------------- DADOS PESSOAIS  CONTIDOS DO TRATAMENTO-------------------------------------------------------------------->
    <div class="col" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="divloco">
                <div class="col-md-12" id="separacao">
                  3. Dados pessoais contidos em cada registo
                </div>
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12">
               
                <div class="col-md-12">
                  <button
                    @click="addRegistro()"
                    alt="Adicionar mais campos"
                    type="button"
                    id="addmore"
                    class="btn btn-success"
                  >
                    <b class="add"
                      ><IconAwe class="icon-color" icon="plus"
                    /></b>
                  </button>
                  <div class="col-md-12"><br /></div>

                  <label for="categorias">
                    Selecione uma Categoria abaixo</label
                  >
                  <div
                    class="row"
                    v-for="(finalidadi, index) in finalidadiCategory"
                    :key="index"
                  >
                    <div class="col-md-4" id="cambs">
                      <Field 
                    :name="'categoria ' + (index + 1)"  
                        as="select"
                        class="form-select" 
                        :rules="validateRadio" 
                        v-model="finalidadi.categoria" 
                        :id="'categoria ' + (index + 1)" 
                        for="categoria"
                        placeholder="- Seleciona uma categoria-"
                      >
                        <option value=""> - selecione uma categoria -</option>
                        <option
                          v-for="categoria in categorias"
                          :key="categoria.id"
                          :value="categoria.value"
                        >
                          {{ categoria.label }}
                        </option>
                      </Field>
                      <ErrorMessage class="errorMessage" :name="'categoria ' + (index + 1)" />
                       </div>
                    <div class="col-md-7" id="cambs">
                      <Multiselect
                        v-model="finalidadi.finalidd"
                        :options="finalidadesCategorias[finalidadi.categoria]"
                        mode="tags"
                        placeholder="- selecione as finalidades -"
                        :close-on-select="true"
                        :searchable="true"
                        :object="true"
                        :multiple="true"
                      />
                    </div>
                    <div class="col-md-1">
                      <button
                        @click="removeRegistro(index)"
                        v-show="index != 0"
                        type="button"
                        id="removeItem"
                        class="btn btn-danger"
                      >
                        <b class="add"
                          ><IconAwe class="icon-color" icon="trash-can"
                        /></b>
                      </button>
                    </div>
                  </div>
                  <div class="col-md-12"><br /></div>
                 
                </div>
              </div>
            </div>
          </div>
        </div>
 
 
        <div class="col" id="divg"> 
              <div class="col-md-12" id="divloco">
                <div class="col-md-12" id="separacao">
                  4. Trabalhadores abrangidos por especial obrigação de sigilo
                </div>
                <div class="col-md-12"><br /></div>
              </div>
              <div class="container">
                <div class="row">
                  <div class="col">
                    <Multiselect
                      v-model="value"
                      name="trabalhadores"
                      id="finalidadetra"
                      placeholder="- Indique os trabalhadores abrangidos por especial obrigação do sigilo-"
                      mode="tags"
                      :close-on-select="false"
                      :searchable="true"
                      :create-option="true"
                      :options="trabalhadorAbra"
                    />
                  </div>
                </div>
              </div> 
        </div>

        <div class="col" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                5.Exercício do direito de acesso às imagens gravadas
              </div>
              <div class="col">
                <label class="form-check-label">
                  Morada do local do exercício do direito de acesso é a mesma
                  indicada em 1?
                </label>
                <buttom
                  @click="changeDireitoAcesso"
                  type="button"
                  class="btn btn-outline-primary"
                  name="morada"
                  id="moradasimbotton"
                >
                  {{ checkDireitoAcesso ? "Sim" : "Não" }}
                </buttom>
              </div>
              <div class="col-md-12" id="divg2" v-if="checkDireitoAcesso">
                <div class="col-md-12">
                  <Field 
                        type="text"
                        class="form-control"
                        name="ruaDireitoAcesso"
                        id="ruaDireitoAcesso"
                        placeholder="Rua do Responsável pelo tratamento"
                      /> 
                </div>
                <div class="col-md-12">
                  <Field 
                        type="text"
                        class="form-control"
                        name="caixaPostalDireitoAcesso"
                        id="caixaPostalDireitoAcesso"
                    placeholder=" Caixa Postal"
                      />  
                </div>
                <div class="col-md-12">
                  <Field
                        :rules="validateText"
                        type="text"
                        class="form-control"
                        name="localDireitoAcesso"
                        id="localDireitoAcesso"
                    placeholder=" Local - Cidade/Vila/Lugar/Zona"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="localDireitoAcesso"
                      />   
                </div>

                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                        as="select"
                        class="form-select"
                        v-model="ilhaDirAcess"
                        name="ilhaDirAcess"
                        id="ilhaDirAcess"
                        for="ilhaDirAcess"
                        :rules="validateRadio"
                        placeholder="- Seleciona uma ilha-"
                      >
                        <option value="">- selecione uma ilha -</option>
                        <option
                          v-for="ilha in ilhas"
                          :key="ilha.value"
                          :value="ilha.value"
                        >
                          {{ ilha.value }}
                        </option>
                      </Field>
                      <ErrorMessage class="errorMessage" name="ilhaDirAcess" />
                    </div>
                    <div class="col">
                      <Field
                        as="select"
                        class="form-select"
                        v-model="concelhoDirAcess"
                        name="concelhoDirAcess"
                        id="concelhoDirAcess"
                        for="concelhoDirAcess"
                        :rules="validateRadio"
                      >
                        <option value="">- selecione um concelho -</option>
                        <option
                          v-for="concelho in concelhos[ilhaDirAcess]"
                          :key="concelho.value"
                          :value="concelho.value"
                        >
                          {{ concelho.value }}
                        </option>
                      </Field>
                      <ErrorMessage
                        class="errorMessage"
                        name="concelhoDirAcess"
                      />

 
                    </div>
                  </div>
                </div>
                <div class="col-md-12"><br /></div>
                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                        :rules="validateEmail"
                        type="email"
                        class="form-control"
                        name="emailDireitoAcesso"
                        id="emailDireitoAcesso"
                        placeholder="Entre o email da pessoa de contato: example@cnpd.cv"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="emailDireitoAcesso"
                      />   
                    </div>
                    <div class="col">
                      <Field
                        :rules="validateNumber"
                        type="text"
                        class="form-control"
                        name="telefoneDireitoAcesso"
                        id="telefoneDireitoAcesso"
                        placeholder="Contato: Telefone/Telemovel"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="telefoneDireitoAcesso"
                      />   
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                De que forma é exercido o direito de acesso?
              </div>
              <div class="col-md-4"></div>
              <div class="col-md-2" id="alignCenter">
                <Field
                  :rules="validateRadio"
                  type="checkbox"
                  id="formaDireitoAcesso"
                  name="formaDireitoAcesso"
                  value="Presencial"
                  v-model="formaDireitoAcesso"
                />
                <label for="formaDireitoAcesso"> Presencial</label>
              </div>
              <div class="col-md-2" id="alignCenter">
                <Field
                  :rules="validateRadio"
                  type="checkbox"
                  id="formaDireitoAcesso"
                  name="formaDireitoAcesso"
                  value="Escrita"
                  v-model="formaDireitoAcesso"
                />
                <label for="formaDireitoAcesso"> Escrita</label>
              </div>
              <div class="col-md-4"></div>
              <div class="col-md-12" id="alignCenter">
                <ErrorMessage class="errorMessage" name="formaDireitoAcesso" />
              </div>

              <div class="col-md-12">
                <Field
                  name="outraFormaDireitoAcesso"
                  as="textarea"
                  class="form-control"
                  v-model="outraFormaDireitoAcesso" 
                  placeholder=" Mencionar outras formas de direito de acesso, caso não for mencionado acima"
                /> 
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                6. Representante dos trabalhadores
              </div>
              <div class="col-md-12"><br /></div>

              <div class="col">
                <label class="form-check-label">
                  Existe representante dos trabalhadores?
                </label>
                <buttom
                  @click="changeRepTrab"
                  type="button"
                  class="btn btn-outline-primary"
                  name="morada"
                  id="moradasimbotton"
                >
                  {{ checkRepTrab ? "Não" : "Sim" }}
                </buttom>
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12" v-if="checkRepTrab">
                <label for="formFile" class="form-label"
                  >Se sim, juntar a cópia do parecer ou comprovativo do
                  pedido.</label
                >
                <input class="form-control" type="file" id="formFile" />
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                7. Medidas de segurança a implementar
              </div>

              <div class="col-md-12">
                <label
                  id="labelleft"
                  class="form-check-label"
                  for="formaDireitoAcesso"
                >
                  Especifique as medidas físicas de segurança do sistema:
                </label>
                <Field
                  name="medidasFisica"
                  as="textarea"
                  class="form-control"
                  v-model="medidasFisica"
                  :rules="validateText"
                  placeholder="Ocorre quando temos barreiras físicas que impeçam que pessoas não autorizadas tenham acesso a espaços onde os dados estão guardados"
                />
                <ErrorMessage class="errorMessage" name="medidasFisica" />
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12">
                <label
                  id="labelleft"
                  class="form-check-label"
                  for="formaDireitoAcesso"
                >
                  Especifique as medidas lógica de segurança do sistema:
                </label>
                <Field
                  name="medidasLogica"
                  as="textarea"
                  class="form-control"
                  v-model="medidasLogica"
                  :rules="validateText"
                  placeholder="Consiste na implementação de chaves de acesso, encriptação do conteúdo e registos de operações efectuadas no sistema"
                />
                <ErrorMessage class="errorMessage" name="medidasFisica" />
              </div>
            </div>
          </div>
        </div>
        
        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">8. Regulamento interno</div>
              <div class="col-md-12"><br /></div>

              <div class="col">
                <label class="form-check-label">
                  Declaro que foi adotado regulamento interno que estabelece as
                  regras de utilização dos meios de comunicação e específica as
                  formas de controlo, em cumprimento dos limites e condições nos
                  termos da lei.
                </label>
                <buttom
                  @click="changeRegInterno"
                  type="button"
                  class="btn btn-outline-primary"
                  name="morada"
                  id="moradasimbotton"
                >
                  {{ checkRegInterno ? "Não" : "Sim" }}
                </buttom>
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12" v-if="checkRegInterno">
                <label for="formFile" class="form-label"
                  >Se sim, juntar a cópia do regulamento interno.</label
                >
                <input class="form-control" type="file" id="formFile" />
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-12"><br /></div>
        <!-- FIM DE FORMS-->
        <div class="col-12" id="divsave">
          <button
            id="buttonsave"
            value="Save"
            class="btn btn-primary"
            type="submit"
          >
          <IconAwe class="icon-color" icon="paper-plane"
                    /> Submeter Dados
          </button>
        </div>
      </Form>
    </div>
  </section>
</template>

<script>
import Multiselect from "@vueform/multiselect";

import { Form, Field, ErrorMessage } from "vee-validate";

export default {
  components: {
    Multiselect,
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    return {
      nomeDenominacao: "",
      checkMorada: false,
      checkServico: false,
      checkServicoSR: false,
      checkDireitoAcesso: false,
      checkComunicTerce: false,
      checkTransfInter: false,
      checkRepTrab: false,
      checkRegInterno: false,

      trabalhadorAbra: [
        { value: "Jornalista", label: "Jornalista" },
        { value: "Profissionais da saúde", label: "Profissionais da saúde" },
        { value: "Advogados", label: "Advogados" },
        { value: "Ministro de culto", label: "Ministro de culto" },
      ],

      finalidadeTratamento: [
        {
          value: "Gestão dos meios da empresa",
          label: "Gestão dos meios da empresa",
        },
        {
          value: "Gestão da produtividade dos trabalhadores",
          label: "Gestão da produtividade dos trabalhadores",
        },
      ],

      /*******************************************TIPO DE NOTIFICAÇÃO ******************************************/
      tipoNotificacao: null,
      tipoNotificacoes: null,
      /**********************************ATIVIDADE DESENVOLVIDA*********************************************** */

      /** *********************ILHAS E CONCELHOS ************************************** */
      ilhaResp: null,
      ilhaMorInst: null,
      ilhaServExt: null,
      ilhaDirAcess: null,
      ilhas: [
        { value: "Santo Antão", label: "Santo Antão" },
        { value: "São Vicente", label: "São Vicente" },
        { value: "São Nicolau", label: "São Nicolau" },
        { value: "Sal", label: "Sal" },
        { value: "Boa Vista", label: "Boa Vista" },
        { value: "Maio", label: "Maio" },
        { value: "Santiago", label: "Santiago" },
        { value: "Fogo", label: "Fogo" },
        { value: "Brava", label: "Brava" },
      ],
      concelho: null,
      concelhoMorInst: null,
      concelhoServExt: null,
      concelhoDirAcess: null,
      ilhaMorRep: null,
      concelhoMorRep: null,
      concelhoResp: null,

      concelhoServExtSR: null,
      ilhaServExtSR: null,
      ilhaRespSR: null,
      concelhoRespSR: null,
      ilhaMorRepSR: null,
      concelhoMorRepSR: null,

      concelhos: {
        "Santo Antão": [
          { value: "Ribeira Grande", label: "Ribeira Grande" },
          { value: "Paul", label: "Paul" },
          { value: "Porto novo", label: "Porto novo" },
        ],
        "São Vicente": [{ value: "São Vicente", label: "São Vicente" }],
        "São Nicolau": [
          { value: "Ribeira Brava", label: "Ribeira Brava" },
          {
            value: "Tarrafal de São Nicolau",
            label: "Tarrafal de São Nicolau",
          },
        ],
        Sal: [{ value: "Sal", label: "Sal" }],
        "Boa Vista": [{ value: "Boa Vista", label: "Boa Vista" }],
        Maio: [{ value: "Maio", label: "Maio" }],
        Santiago: [
          { value: "Praia", label: "Praia" },
          { value: "São Domingos", label: "São Domingos" },
          { value: "Santa Catarina", label: "Santa Catarina" },
          { value: "São Salvador do Mundo", label: "São Salvador do Mundo" },
          { value: "Santa Cruz", label: "Santa Cruz" },
          {
            value: "São Lourenço dos Órgãos",
            label: "São Lourenço dos Órgãos",
          },
          {
            value: "Ribeira Grande de Santiago",
            label: "Ribeira Grande de Santiago",
          },
          { value: "São Miguel", label: "São Miguel" },
          { value: "Tarrafal", label: "Tarrafal" },
        ],
        Fogo: [
          { value: "São Filipe", label: "São Filipe" },
          { value: "Santa Catarina do Fogo", label: "Santa Catarina do Fogo" },
          { value: "Mosteiros", label: "Mosteiros" },
        ],
        Brava: [{ value: "Brava", label: "Brava" }],
      },
      /*****************************CATEGORIA E FINALIDADES DE TRATAMENTO************************************** */
      selected: {},
      finalidd: null,
      categoria: null,

      categorias: [
        {
          id: 1,
          value: "Telefone",
          label: "Telefone",
        },
        {
          id: 2,
          value: "Correio electrónico",
          label: "Correio electrónico",
        },
        {
          id: 3,
          value: "Internet",
          label: "Internet",
        },
      ],

      finalidadesCategorias: {
        "Telefone": [
          {
            id: 1,
            value: "Telefone fixo",
            label: "Telefone fixo",
          },
          {
            id: 1,
            value: "Telefone móvel",
            label: "Telefone móvel",
          },
          {
            id: 1,
            value: "Utilizador",
            label: "Utilizador",
          },
          {
            id: 1,
            value: "Categoria/função",
            label: "Categoria/função",
          },
          {
            id: 1,
            value:
              "Número de telefone chamado, com supressão dos últimos quatro dítigos",
            label:
              "Número de telefone chamado, com supressão dos últimos quatro dítigos",
          },
          {
            id: 1,
            value: "Tipo de chamada(local, regional e internacional)",
            label: "Tipo de chamada(local, regional e internacional)",
          },
          {
            id: 1,
            value: "Duração da chamada",
            label: "Duração da chamada",
          },
          {
            id: 1,
            value: "Custo da comunicação",
            label: "Custo da comunicação",
          },
        ],

        "Correio electrónico": [
          {
            id: 1,
            value: "Endereço do destinatário",
            label: "Endereço do destinatário",
          },
          {
            id: 1,
            value: "Endereço do remetente",
            label: "Endereço do remetente",
          },
          {
            id: 1,
            value: "Assunto",
            label: "Assunto",
          },
          {
            id: 1,
            value: "Data e hora de envio",
            label: "Data e hora de envio",
          },
          {
            id: 1,
            value: "Tipos de ficheiros anexados(EXE, MP3, AVI etc)",
            label: "Tipos de ficheiros anexados(EXE, MP3, AVI etc)",
          },
        ],
        "Internet": [
          {
            id: 1,
            value: "Utilizador",
            label: "Utilizador",
          },
          {
            id: 2,
            value: "Data e hora de inicio e fim da conexão",
            label: "Data e hora de inicio e fim da conexão",
          },
        ],
      }, 
      /************************************CATEGORIA DE FINALIDADE*********************************** */
      finalidadiCategory: [
        {
          categoria: "",
          finalidadesCategorias: "",
        },
      ],
 
      /**************************************************************************************************** */
    };
  },

  methods: {
    onSubmit(values) {
      console.log(values, null, 2);
      
    },
    validateText(value) {
      // if the field is empty
      if (!value) {
        return "Campo obrigatório!";
      }
      return true;
    },

    validateRadio(value) {
      // if the field is empty
      if (!value) {
        return "Precisa selecionar uma opção!";
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
        return "Carater inválido, Precisa ser um número!";
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
    },

     
    async dadosBackend() {
      const req = await fetch("http://localhost:3000/dadosBackend");
      const data = await req.json(); 
      this.ilhas = data.ilhas;
      this.atividadesDesenvolvidas = data.atividadesDesenvolvidas;
      this.tipoNotificacoes = data.tipoNotificacoes; 
      
    },
     
    /*FINALIDADES MULTIPLAS*/

    addRegistro() {
      this.finalidadiCategory.push({
        categoria: "",
        finalidadesCategorias: "",
      });
    },
    removeRegistro(index) {
      this.finalidadiCategory.splice(index, 1);
    },
    changeServico() {
      this.checkServico = !this.checkServico;
    },
    changeServicoSR() {
      this.checkServicoSR = !this.checkServicoSR;
    },
    changeDireitoAcesso() {
      this.checkDireitoAcesso = !this.checkDireitoAcesso;
    },

    changeComunicTerce() {
      this.checkComunicTerce = !this.checkComunicTerce;
    },
    changeTransfInter() {
      this.checkTransfInter = !this.checkTransfInter;
    },
    changeRepTrab() {
      this.checkRepTrab = !this.checkRepTrab;
    },
    changeRegInterno() {
      this.checkRegInterno = !this.checkRegInterno;
    },
  },
  mounted() {
    this.dadosBackend();
  },

  watch: {
    categoria() {
      this.finalidd = null;
    },
    tipoVideo() {
      this.zona = null;
    },
  },
};
</script>

<style>
#alignCenter{
  text-align: center;
}
#cambs {
  margin-top: 5px;
}
.add {
  font-size: 16px;
  font-family: "Times New Roman", Times, serif;
}
.Interconexao {
  font-family: "Times New Roman", Times, serif;
  padding-top: 110px;
}
.container {
  font-family: "Times New Roman", Times, serif;
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
#divg {
  font-family: "Times New Roman", Times, serif;
  border: 1px solid #061536;
  padding: 10px;
  border-radius: 10px;
}
.col {
  font-family: "Times New Roman", Times, serif;
}
#divg2 {
  font-family: "Times New Roman", Times, serif;
  padding-top: 20px;
}
.col,
.row {
  font-family: "Times New Roman", Times, serif;
}
input,
label,
textarea {
  font-family: "Times New Roman", Times, serif;
}
input {
  margin-bottom: 10px;
}
input.form-control:focus,
select.form-select:focus,
textarea.form-control:focus {
  outline: none !important;
  border-color: #061536;
  box-shadow: 0 0 10px #061536;
}
option:hover {
  background-color: #061536;
}
.form-check-input:checked {
  background-color: #061536;
}

.form-check-input:checked + label {
  color: #061536;
}

#separacao {
  font-family: "Times New Roman", Times, serif;
  padding-left: 10px;
  text-align: center;
  color: #ffffff;
  border-style: ridge;
  border-radius: 10px;
  background: #061536;
}
#separacao1 {
  font-family: "Times New Roman", Times, serif;
  padding-left: 10px;
  color: #061536;
  font-weight: bold;
}
#labelleft {
  text-align: left;
}
#divloco {
  margin-top: 10px;
}
#moradasimbotton {
  margin-left: 10px;
  color: #061536;
  border-color: #061536;
}
#moradasimbotton:hover {
  background-color: #061536;
  color: #fff;
  border: 2px solid #bd9a13;
}

.icon-box {
  background-color: white;
}
#buttonsave {
  background-color: #061536;
}
#divsave {
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
 

</style>
