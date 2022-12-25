<template>
  <section id="GEO" class="GEO">
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
          <router-link style="text-decoration: none" to="/formscctv">
            <b>Formulário de Geolocalização de Viaturas no Contexto Laboral - GPS</b>
          </router-link>
        </h5>
      </div>
      <Form @submit="onSubmit">
        <!-- FORMS GEO-->
        <div class="section-title">
          <h2>NOTIFICAÇÃO DE GEOLOCALIZAÇÃO DE VIATURAS NO CONTEXTO LABORAL</h2>
        </div>
        
        <div class="col-md-12" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-2">
                <label id="labelleft" for="TipoNot" class="form-label"
                  >Tipo Notificação</label> 
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
              
              <div class="row">
                <div class="col-md-12" id="divloco">
                <div class="col-md-12" id="separacao">
                  1. Responsável pelo Tratamento
                  <br />
                </div>
                <div class="col-md-12"><br></div> 
              </div> 
              <div class="col-md-4"></div>
              <div class="col-md-2">
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
              <div class="col-md-2">
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
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="nomeDenominacao"
                  id="nomeDenominacao"
                  alt="Nome Denominação: Refere-se à designação oficial de uma instituição pública ou privada"
                  placeholder=" Nome/Denominação"
                />
                <ErrorMessage class="errorMessage" name="nomeDenominacao" />
              </div>

              <div class="col-md-12">
                <Field 
                  type="text"
                  class="form-control"
                  name="nomeComercial"
                  id="nomeComercial"
                  alt="Nome comercial: Pode ser a sigla ou designação em relação ao qual a instituição é mais conhecida."
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
                  <option value="">selecione a atividade desenvolvida</option>
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
                  :rules="validateNumber"
                  type="text"
                  class="form-control"
                  name="nifResp"
                  id="nifResp"
                  alt="NIF"
                  placeholder="Númercbnm,o de NIF"
                />
                <ErrorMessage class="errorMessage" name="nifResp" />
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <Field 
                      type="text"
                      class="form-control"
                      name="ruaResp"
                      id="ruaResp"
                      alt="RUA"
                      placeholder="Entre o nome da Rua"
                    /> 
                  </div>
                  <div class="col">
                    <Field
                      :rules="validateText"
                      type="text"
                      class="form-control"
                      name="localResp"
                      id="localResp"
                      alt="Local"
                      placeholder="Cidade/Vila/Lugar/Zona"
                    />
                    <ErrorMessage class="errorMessage" name="localResp" />
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
                      :rules="validateRadio"
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
                      :rules="validateRadio"
                    >
                      <option value="">- selecione um concelho -</option>
                      <option
                        v-for="concelho in concelhos[ilhaResp]"
                        :key="concelho.value"
                        :value="concelho.value"
                      >
                        {{ concelho.value }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="concelhoResp" />
                  </div>
                </div>
              </div>
              <div class="col-md-12" id="divloco">
                <div class="row">
                  <div class="col">
                    <Field 
                      type="text"
                      class="form-control"
                      name="caixaPostalResp"
                      id="caixaPostalResp"
                      alt="Caixa Postal"
                      placeholder="Entre o número da Caixa Postal"
                    /> 
                  </div>
                  <div class="col">
                    <Field
                      :rules="validateNumber"
                      v-model="telefoneResp"
                      type="text"
                      class="form-control"
                      name="telefoneResp"
                      id="telefoneResp"
                      alt="Telefone/Telemovel"
                      placeholder="Contato: Telefone/Telemovel"
                    />
                    <ErrorMessage class="errorMessage" name="telefoneResp" />
                  </div>
                </div>
              </div>
              <div class="col-md-12">
                <div class="row">
                  <div class="col">
                    <Field
                      :rules="validateEmail"
                      type="email"
                      class="form-control"
                      name="emailResp"
                      id="emailResp"
                      placeholder="Entre o seu email: example@cnpd.cv"
                    />
                    <ErrorMessage class="errorMessage" name="emailResp" />
                  </div>
                  <div class="col">
                    <div class="col">
                      <Field
                        :rules="validateRadio"
                        type="radio"
                        id="paisResp"
                        name="paisResp"
                        value="Cabo Verde"
                        v-model="paisResp"
                      />
                      <label for="Pessoa Singular"> Cabo Verde</label>
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
                      <label for=" Fora do Território Nacional">
                        Fora do Território Nacional</label
                      >
                    </div>
                    <ErrorMessage class="errorMessage" name="paisResp" />
                  </div>
                </div>
              </div>
            </div> 
              <div class="col-md-12">
                <Field
                      :rules="validateText"
                      type="text"
                      class="form-control"
                      name="representante"
                      id="representante"
                  placeholder=" Representante"
                    />
                    <ErrorMessage class="errorMessage" name="representante" /> 
              </div>
              <div class="col">
                <Field 
                      type="text"
                      class="form-control"
                      name="ruaRep"
                      id="ruaRep"
                  placeholder=" Rua "
                    />  
              </div>
              <div class="col">
              
                <Field 
                      type="text"
                      class="form-control"
                      name="caixaPostalRep"
                      id="caixaPostalRep"
                  placeholder=" Caixa Postal "
                    />  
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
                      :rules="validateRadio"
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
                      :rules="validateRadio"
                    >
                      <option value="">- selecione um concelho -</option>
                      <option
                        v-for="concelho in concelhos[ilhaMorRep]"
                        :key="concelho.value"
                        :value="concelho.value"
                      >
                        {{ concelho.value }}
                      </option>
                    </Field>
                    <ErrorMessage class="errorMessage" name="concelhoMorRep" /> 
                  </div>
                </div>
              </div>
              <div class="col-md-12" id="divloco">
                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                      :rules="validateText"
                      type="text"
                      class="form-control"
                      name="localMoradaRep"
                      id="localMoradaRep"
                        placeholder="Cidade/Vila/Lugar/Zona"
                    />
                    <ErrorMessage class="errorMessage" name="localMoradaRep" />  
                    </div>
                    <div class="col">
                      <input
                        disabled
                        type="text"
                        class="form-control"
                        name="paisRep"
                        value="Cabo Verde"
                        id="paisRep"
                        placeholder="Cabo Verde"
                      />
                    </div>
                  </div>
                </div> 
                <div class="col-md-12">
                  <Field
                      :rules="validateText"
                      type="text"
                      class="form-control"
                      name="nomePessoaContato"
                      id="nomePessoaContato"
                    placeholder="Nome da pessoa de contato"
                    />
                    <ErrorMessage class="errorMessage" name="nomePessoaContato" />   
                </div>

                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                      :rules="validateEmail"
                      type="text"
                      class="form-control"
                      name="emailMoradaRep"
                      id="emailMoradaRep"
                        placeholder="Entre o email da pessoa de contato: example@cnpd.cv"
                    />
                    <ErrorMessage class="errorMessage" name="emailMoradaRep" />  
                    </div>
                    <div class="col">
                      <Field
                      :rules="validateNumber"
                      type="text"
                      class="form-control"
                      name="telefoneMorRep"
                      id="telefoneMorRep"
                        placeholder="Contato: Telefone/Telemovel"
                    />
                    <ErrorMessage class="errorMessage" name="telefoneMorRep" />   
                    </div>
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
                  <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="ruaProcessInfo"
                  id="ruaProcessInfo"
                    placeholder=" Rua"
                />
                <ErrorMessage class="errorMessage" name="ruaProcessInfo" />  
                </div>
                <div class="col-md-12">
                  <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="caixaPostalProcessInfo"
                  id="caixaPostalProcessInfo"
                    placeholder=" Caixa Postal"
                />
                <ErrorMessage class="errorMessage" name="caixaPostalProcessInfo" />  
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

        <!---- ----------------- Finalidade e Categoria de dados Pesoais-------------------------------------------------------------------->

        <div class="col" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                2. Finalidades do Tratamento
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12"> 
                <label class="form-check-label"> 
                  Indique a(s) finalidade(s) do tratamento de dados
                </label>
                <treeselect
                  :multiple="true"
                  :options="finalidadesTratamento"
                  :disable-branch-nodes="true"
                  placeholder="- Selecione as finalidades - "
                  v-model="finalidade"
                  search-nested
                />

                <!--<pre class="language-json"><code>{{finalidade}}</code></pre>-->
              </div>

              <div class="col-md-12"><br /></div>
              <div class="col">
                <label class="form-check-label"> 
                  Categorias dos dados pessoais tratados
                </label> 
                 
                <treeselect
                  :multiple="true"
                  :options="categoriasDados"
                  placeholder="- Selecione as categorias de dados - "
                  v-model="categoria"
                />
                <!--<pre class="language-json"><code>{{categoria}}</code></pre>-->
              </div>
              <div class="col">
                <label class="form-check-label"> 
                  Outros dados pessoais tratados
                </label>  
                <treeselect
                  :multiple="true"
                  :options="outrosDadosTratados"
                  :disable-branch-nodes="true"
                  placeholder="- Selecione os dados tratados - "
                  v-model="outrosDadosTratado"
                  search-nested
                />

                <!--<pre class="language-json"><code>{{outrosDadosTratado}}</code></pre>-->
              </div>
              <div class="col-md-12"><br /></div>
            </div>
          </div>
        </div>
        <div class="col" id="divg">
          <div class="container">
            <div class="row">
              <div class="col-md-12" id="separacao">
                3.Exercício do direito de acesso às imagens gravadas
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
                4. Medidas de segurança a implementar
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
              <div class="col-md-12" id="separacao">
                5. Representante dos trabalhadores
              </div>
              <div class="col-md-12">
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
      </form>
    </div>
  </section>
</template>

<script>  
// import the component
import Treeselect from "vue3-treeselect";
// import the styles
import "vue3-treeselect/dist/vue3-treeselect.css";
import { Form, Field, ErrorMessage } from "vee-validate";

export default {
  components: {
    Treeselect, 
    Form,
    Field,
    ErrorMessage,
  },
 
  data() {
    return {
      nomeDenominacao: "",
      checkMorada: false,
      checkServico: false,
      checkDireitoAcesso: false,
      checkRepTrab: false,

      /**************************TIPO NOTIFICACAO *********************************** */
     tipoNotificacao:null,
    tipoNotificacoes:null,

      /**********************************ATIVIDADE DESENVOLVIDA*********************************************** */
      atividade:null,
      atividadeSR:null,
      atividadesDesenvolvidas:null, 

      /******************************FINALIDADES E CATEGORIA DO TRATAMENTO*******************************/
      //FINALIDADE
      finalidade: [],
      finalidadesTratamento: [
        {
          id: "Gestão da frota em serviço",
          label: "Gestão da frota em serviço",
          children: [
            {
              id: "Assistência técnica externa/ao domicílio",
              label: "Assistência técnica externa/ao domicílio",
            },
            {
              id: "Transporte público de passageiros",
              label: "Transporte público de passageiros",
            },
            {
              id: "Transporte de mercadorias",
              label: "Transporte de mercadorias",
            },
            {
              id: "Destribuição de bens",
              label: "Destribuição de bens",
            },
            {
              id: "Segurança privada",
              label: "Segurança privada",
            },
          ],
        },
        {
          id: "Proteção de pessoas e carga de materiais perigosos",
          label: "Proteção de pessoas e carga de materiais perigosos",
        },
        {
          id: "Proteção de carga de materiais de valor",
          label: "Proteção de carga de materiais de valor",
        },
        {
          id: "Participação criminal em caso de furto",
          label: "Participação criminal em caso de furto",
        },
      ],
      //CATEGORIA DE DADOS
      categoria: [],
      categoriasDados: [
        {
          id: "Dados de geolocalização de viatura",
          label: "Dados de geolocalização de viatura",
        },
        {
          id: "Dados relativos à identificação do veículo",
          label: "Dados relativos à identificação do veículo",
        },
        {
          id: "Dados de identificação dos trabalhadores",
          label: "Dados de identificação dos trabalhadores",
        },
      ],
      //OUTROS DADOS TRATADOS
      outrosDadosTratado: [],
      outrosDadosTratados: [
        {
          id: "Outros dados para gestão de frota em serviço externo:",
          label: "Outros dados para gestão de frota em serviço externo:",
          children: [
            {
              id: 1,
              value: "Dados letaivos ao serviço a prestar",
              label: "Dados letaivos ao serviço a prestar",
            },
            {
              id: 2,
              value: "Dados relativos à carga transportada",
              label: "Dados relativos à carga transportada",
            },
          ],
        },
        {
          id: "Outros dados para proteção de pessoas e carga de materiais perigosos",
          label:
            "Outros dados para proteção de pessoas e carga de materiais perigosos",
          children: [
            {
              id: 3,
              value: "Dados relativos ao transsporte",
              label: "Dados relativos ao transsporte",
            },
            {
              id: 4,
              value: "Percurso previsto",
              label: "Percurso previsto",
            },
            {
              id: 5,
              value: "Carga transportada",
              label: "Carga transportada",
            },
            {
              id: 6,
              value: "Procedimentos de segurança e/ou emergência adotados",
              label: "Procedimentos de segurança e/ou emergência adotados",
            },
          ],
        },
        {
          id: "Outros dados para a proteção de carga de materiais de valor:",
          label: "Outros dados para a proteção de carga de materiais de valor:",
          children: [
            {
              id: 7,
              value: "Caraterśticas da viatura",
              label: "Caraterśticas da viatura",
            },
            {
              id: 8,
              value: "Dados relativos ao transporte",
              label: "Dados relativos ao transporte",
            },
            {
              id: 9,
              value: "Percurso previsto",
              label: "Percurso previsto",
            },
            {
              id: 10,
              value: "Carga transportada",
              label: "Carga transportada",
            },
            {
              id: 11,
              value: "Procedimentos de segurança e/ou emergência adotados",
              label: "Procedimentos de segurança e/ou emergência adotados",
            },
          ],
        },
      ],

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

      /** *********************************************************** */
    };
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
    },

    async dadosBackend(){
      const req = await fetch("http://localhost:3000/dadosBackend");
      const data= await req.json(); 
      this.ilhas = data.ilhas;
      this.atividadesDesenvolvidas = data.atividadesDesenvolvidas;
      this.categorias = data.categorias;
      this.tipoNotificacoes = data.tipoNotificacoes;
      
    },

    changeServico() {
      this.checkServico = !this.checkServico;
    },
    changeDireitoAcesso() {
      this.checkDireitoAcesso = !this.checkDireitoAcesso;
    },

    changeRepTrab() {
      this.checkRepTrab = !this.checkRepTrab;
    },
  },

  mounted() {
    this.dadosBackend();
  },
};
</script>

<style>
.GEO {
  font-family: "Times New Roman", Times, serif;;
  padding-top: 110px;
}
.container {
  font-family: "Times New Roman", Times, serif;;
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
  font-family: "Times New Roman", Times, serif;;
  border: 1px solid #061536;
  padding: 10px;
  border-radius: 10px;
}
.col {
  font-family: "Times New Roman", Times, serif;;
}
#divg2 {
  font-family: "Times New Roman", Times, serif;;
  padding-top: 20px;
}
.col,
.row {
  font-family: "Times New Roman", Times, serif;;
}
input,
label,
textarea {
  font-family: "Times New Roman", Times, serif;;
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
  font-family: "Times New Roman", Times, serif;;
  padding-left: 10px;
  text-align: center;
  color: #ffffff;
  border-style: ridge;
  border-radius: 10px;
  background: #061536;
}
#separacao1 {
  font-family: "Times New Roman", Times, serif;;
  padding-left: 10px;
  color: #061536;
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
