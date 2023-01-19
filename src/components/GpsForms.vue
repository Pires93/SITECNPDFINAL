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
            <b
              >Formulário de Geolocalização de Viaturas no Contexto Laboral -
              GPS</b
            >
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
              <div class="row">
                <div class="col-md-12" id="divloco">
                  <div class="col-md-12" id="separacao">
                    1. Responsável pelo Tratamento
                    <br />
                  </div>
                  <div class="col-md-12"><br /></div>
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
                    name="nome_denominacao"
                    id="nome_denominacao"
                    v-model="nome_denominacao"
                    placeholder=" Nome/Denominação"
                  />
                  <ErrorMessage class="errorMessage" name="nome_denominacao" />
                </div>

                <div class="col-md-12">
                  <Field
                    type="text"
                    class="form-control"
                    name="nome_comercial"
                    id="nome_comercial"
                    v-model="nome_comercial"
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
                    type="number"
                    class="form-control"
                    name="numero_nif"
                    id="numero_nif"
                    v-model="numero_nif"
                    placeholder="Número de NIF"
                  />
                  <ErrorMessage class="errorMessage" name="numero_nif" />
                </div>
                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                        type="text"
                        class="form-control"
                        name="rua_responsavel_tratamento"
                        id="rua_responsavel_tratamento"
                        v-model="rua_responsavel_tratamento"
                        placeholder="Entre o nome da Rua"
                      />
                    </div>
                    <div class="col">
                      <Field
                        :rules="validateText"
                        type="text"
                        class="form-control"
                        name="local_responsavel_tratamento"
                        id="local_responsavel_tratamento"
                        v-model="local_responsavel_tratamento"
                        placeholder="Cidade/Vila/Lugar/Zona"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="local_responsavel_tratamento"
                      />
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
                        name="caixapostal_responsavel_tratamento"
                        id="caixapostal_responsavel_tratamento"
                        v-model="caixapostal_responsavel_tratamento"
                        placeholder="Entre o número da Caixa Postal"
                      />
                    </div>
                    <div class="col">
                      <Field
                        :rules="validateNumber"
                        v-model="telefone_responsavel_tratamento"
                        type="number"
                        class="form-control"
                        name="telefone_responsavel_tratamento"
                        id="telefone_responsavel_tratamento"
                        alt="Telefone/Telemovel"
                        placeholder="Contato: Telefone/Telemovel"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="telefone_responsavel_tratamento"
                      />
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
                        name="email_responsavel_tratamento"
                        id="email_responsavel_tratamento"
                        v-model="email_responsavel_tratamento"
                        placeholder="Entre o seu email: example@cnpd.cv"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="email_responsavel_tratamento"
                      />
                    </div>
                    <div class="col">
                      <div class="col">
                        <Field
                          :rules="validateRadio"
                          type="radio"
                          id="pais_responsavel_tratamento"
                          name="pais_responsavel_tratamento"
                          value="Cabo Verde"
                          v-model="pais_responsavel_tratamento"
                        />
                        <label for="Pessoa Singular"> Cabo Verde</label>
                      </div>
                      <div class="col">
                        <Field
                          :rules="validateRadio"
                          type="radio"
                          id="pais_responsavel_tratamento"
                          name="pais_responsavel_tratamento"
                          value=" Fora do Território Nacional"
                          v-model="pais_responsavel_tratamento"
                        />
                        <label for=" Fora do Território Nacional">
                          Fora do Território Nacional</label
                        >
                      </div>
                      <ErrorMessage
                        class="errorMessage"
                        name="pais_responsavel_tratamento"
                      />
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-md-12">
                <Field
                  :rules="validateText"
                  type="text"
                  class="form-control"
                  name="nome_representante_instalacao"
                  id="nome_representante_instalacao"
                  v-model="nome_representante_instalacao"
                  placeholder=" Representante"
                />
                <ErrorMessage
                  class="errorMessage"
                  name="nome_representante_instalacao"
                />
              </div>
              <div class="col">
                <Field
                  type="text"
                  class="form-control"
                  name="rua_representante_instalacao"
                  id="rua_representante_instalacao"
                  placeholder=" Rua "
                  v-model="rua_representante_instalacao"
                />
              </div>
              <div class="col">
                <Field
                  type="text"
                  class="form-control"
                  name="caixapostal_representante_instalacao"
                  id="caixapostal_representante_instalacao"
                  v-model="caixapostal_representante_instalacao"
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
                        name="local_representante_instalacao"
                        id="local_representante_instalacao"
                        v-model="local_representante_instalacao"
                        placeholder="Cidade/Vila/Lugar/Zona"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="local_representante_instalacao"
                      />
                    </div>
                    <div class="col">
                      <input
                        disabled
                        type="text"
                        class="form-control"
                        name="paisRep"
                        id="paisRep"
                        v-model="paisRep"
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
                    name="nome_pessoa_contato_representante_instalacao"
                    id="nome_pessoa_contato_representante_instalacao"
                    placeholder="Nome da pessoa de contato"
                    v-model="nome_pessoa_contato_representante_instalacao"
                  />
                  <ErrorMessage
                    class="errorMessage"
                    name="nome_pessoa_contato_representante_instalacao"
                  />
                </div>

                <div class="col-md-12">
                  <div class="row">
                    <div class="col">
                      <Field
                        :rules="validateEmail"
                        type="text"
                        class="form-control"
                        name="email_pessoa_representante_instalacao"
                        id="email_pessoa_representante_instalacao"
                        v-model="email_pessoa_representante_instalacao"
                        placeholder="Entre o email da pessoa de contato: example@cnpd.cv"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="email_pessoa_representante_instalacao"
                      />
                    </div>
                    <div class="col">
                      <Field
                        :rules="validateNumber"
                        type="number"
                        class="form-control"
                        name="contato_representante_instalacao"
                        id="contato_representante_instalacao"
                        placeholder="Contato: Telefone/Telemovel"
                        v-model="contato_representante_instalacao"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="contato_representante_instalacao"
                      />
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
              <div class="col-md-12" v-if="checkServico">
                <div class="col-md-12">
                  <Field
                    :rules="validateText"
                    type="text"
                    class="form-control"
                    name="entidade_processamento_informacao"
                    id="entidade_processamento_informacao"
                    v-model="entidade_processamento_informacao"
                    placeholder=" Qual a Entidade Encarregue pelo proccessamento das imagens"
                  />
                  <ErrorMessage
                    class="errorMessage"
                    name="entidade_processamento_informacao"
                  />
                </div>
                <div class="col-md-12">
                  <Field
                    type="text"
                    class="form-control"
                    name="rua_processamento_informacao"
                    id="rua_processamento_informacao"
                    v-model="rua_processamento_informacao"
                    placeholder=" Rua"
                  />
                </div>
                <div class="col-md-12">
                  <Field
                    type="text"
                    class="form-control"
                    name="caixapostal_processamento_informacao"
                    id="caixapostal_processamento_informacao"
                    v-model="caixapostal_processamento_informacao"
                    placeholder=" Caixa Postal"
                  />
                </div>
                <div class="col-md-12">
                  <Field
                    :rules="validateText"
                    type="text"
                    class="form-control"
                    name="local_processamento_informacao"
                    id="local_processamento_informacao"
                    v-model="local_processamento_informacao"
                    placeholder="Cidade/Vila/Lugar/Zona da Entidade"
                  />
                  <ErrorMessage
                    class="errorMessage"
                    name="local_processamento_informacao"
                  />
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
                      <ErrorMessage
                        class="errorMessage"
                        name="concelhoServExt"
                      />
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
        <!--------------------------------DIREITO ACESSO---------------------------->
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
                    name="rua_direito_acesso"
                    id="rua_direito_acesso"
                    v-model="rua_direito_acesso"
                    placeholder="Rua do Responsável pelo tratamento"
                  />
                </div>
                <div class="col-md-12">
                  <Field
                    type="text"
                    class="form-control"
                    name="caixapostal_direito_acesso"
                    id="caixapostal_direito_acesso"
                    v-model="caixapostal_direito_acesso"
                    placeholder=" Caixa Postal"
                  />
                </div>
                <div class="col-md-12">
                  <Field
                    :rules="validateText"
                    type="text"
                    class="form-control"
                    name="local_direito_acesso"
                    id="local_direito_acesso"
                    v-model="local_direito_acesso"
                    placeholder=" Local - Cidade/Vila/Lugar/Zona"
                  />
                  <ErrorMessage
                    class="errorMessage"
                    name="local_direito_acesso"
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
                        name="email_direito_acesso"
                        id="email_direito_acesso"
                        v-model="email_direito_acesso"
                        placeholder="Entre o email da pessoa de contato: example@cnpd.cv"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="email_direito_acesso"
                      />
                    </div>
                    <div class="col">
                      <Field
                        :rules="validateNumber"
                        type="number"
                        class="form-control"
                        name="contato_direito_acesso"
                        id="contato_direito_acesso"
                        placeholder="Contato: Telefone/Telemovel"
                      />
                      <ErrorMessage
                        class="errorMessage"
                        name="contato_direito_acesso"
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
                  id="forma_direito_acesso"
                  name="forma_direito_acesso"
                  value="Presencial"
                  v-model="forma_direito_acesso"
                />
                <label> Presencial</label>
              </div>
              <div class="col-md-2" id="alignCenter">
                <Field
                  :rules="validateRadio"
                  type="checkbox"
                  id="forma_direito_acesso"
                  name="forma_direito_acesso"
                  value="Escrita"
                  v-model="forma_direito_acesso"
                />
                <label> Escrita</label>
              </div>

              <div class="col-md-12" id="alignCenter">
                <ErrorMessage
                  class="errorMessage"
                  name="forma_direito_acesso"
                />
              </div>
              <div class="col-md-12">
                <Field
                  name="outraforma_direito_acesso"
                  as="textarea"
                  class="form-control"
                  v-model="outraforma_direito_acesso"
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
                <label id="labelleft" class="form-check-label">
                  Especifique as medidas físicas de segurança do sistema:
                </label>
                <Field
                  name="medidas_fisicas_seguranca"
                  as="textarea"
                  class="form-control"
                  v-model="medidas_fisicas_seguranca"
                  :rules="validateText"
                  placeholder="Ocorre quando temos barreiras físicas que impeçam que pessoas não autorizadas tenham acesso a espaços onde os dados estão guardados"
                />
                <ErrorMessage
                  class="errorMessage"
                  name="medidas_fisicas_seguranca"
                />
              </div>
              <div class="col-md-12"><br /></div>
              <div class="col-md-12">
                <label id="labelleft" class="form-check-label">
                  Especifique as medidas lógica de segurança do sistema:
                </label>
                <Field
                  name="medidas_logicas_seguranca"
                  as="textarea"
                  class="form-control"
                  v-model="medidas_logicas_seguranca"
                  :rules="validateText"
                  placeholder="Consiste na implementação de chaves de acesso, encriptação do conteúdo e registos de operações efectuadas no sistema"
                />
                <ErrorMessage
                  class="errorMessage"
                  name="medidas_logicas_seguranca"
                />
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
                  >Se sim, juntar a cópia do parecer ou comprovativo do pedido
                  em formato PDF.</label
                >
                <Field
                  v-model="parecer_representante_trabalhadores"
                  name="parecer_representante_trabalhadores"
                  class="form-control"
                  type="file"
                  ref="file"
                  :rules="validateText"
                />
                <ErrorMessage
                  class="errorMessage"
                  name="parecer_representante_trabalhadores"
                />
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
            <IconAwe class="icon-color" icon="paper-plane" /> Submeter Dados
          </button>
        </div>
      </Form>
    </div>
  </section>
</template>

<script>
// import the component
import Treeselect from "vue3-treeselect";
// import the styles
import "vue3-treeselect/dist/vue3-treeselect.css";
import { Form, Field, ErrorMessage } from "vee-validate";

import axios from "axios";
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
      tipoNotificacao: null,
      tipoNotificacoes: null,

      /**********************************ATIVIDADE DESENVOLVIDA*********************************************** */
      atividade: null,
      atividadeSR: null,
      atividadesDesenvolvidas: null,

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
              id: "Dados retaivos ao serviço a prestar",
              value: "Dados retaivos ao serviço a prestar",
              label: "Dados retaivos ao serviço a prestar",
            },
            {
              id: "Dados relativos à carga transportada",
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
              id: "Dados relativos ao transporte",
              value: "Dados relativos ao transporte",
              label: "Dados relativos ao transporte",
            },
            {
              id:"Percurso previsto",
              value: "Percurso previsto",
              label: "Percurso previsto",
            },
            {
              id: "Carga transportada",
              value: "Carga transportada",
              label: "Carga transportada",
            },
            {
              id: "Procedimentos de segurança e/ou emergência adotados",
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
              id: "Carateristicas da viatura",
              value: "Carateristicas da viatura",
              label: "Carateristicas da viatura",
            },
            {
              id: "Dados relativos ao transporte",
              value: "Dados relativos ao transporte",
              label: "Dados relativos ao transporte",
            },
            {
              id: "Percurso previsto",
              value: "Percurso previsto",
              label: "Percurso previsto",
            },
            {
              id: "Carga transportada",
              value: "Carga transportada",
              label: "Carga transportada",
            },
            {
              id: "Procedimentos de segurança e/ou emergência adotados",
              value: "Procedimentos de segurança e/ou emergência adotados",
              label: "Procedimentos de segurança e/ou emergência adotados",
            },
          ],
        },
      ],

      /** *********************ILHAS E CONCELHOS ************************************** */
      ilhaResp: null,
      ilhaMorRep: null,
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
      concelhoMorRep: null,
      concelhoServExt: null,
      concelhoDirAcess: null,
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
      nome_denominacao: "",
      nome_comercial: "",
      tipo_notificacao: "",
      tipo_pessoa: "",
      atividade_desenvolvida: "",
      numero_nif: "",
      rua_responsavel_tratamento: "",
      local_responsavel_tratamento: "",
      telefone_responsavel_tratamento: "",
      email_responsavel_tratamento: "",
      pais_responsavel_tratamento: "",
      nome_representante_instalacao: "",
      email_pessoa_representante_instalacao: "",
      contato_representante_instalacao: "",
      rua_representante_instalacao: "",
      caixapostal_representante_instalacao: "",
      local_representante_instalacao: "", 
      nome_pessoa_contato_representante_instalacao: "",
      ilha_responsavel_tratamento: "",
      concelho_responsavel_tratamento: "",
      caixapostal_responsavel_tratamento: "",

      entidade_processamento_informacao: "",
      rua_processamento_informacao: "",
      caixapostal_processamento_informacao: "",
      local_processamento_informacao: "",
      ilha_processamento_informacao: "",
      concelho_processamento_informacao: "",
      finalidadeTratamento: "",
      categoriaDados: "",
      outrosDados: "",
      paisRep:"",
      rua_direito_acesso: "",
      caixapostal_direito_acesso: "",
      local_direito_acesso: "",
      email_direito_acesso: "",
      contato_direito_acesso: "",
      ilha_direito_acesso: "",
      concelho_direito_acesso: "",
      forma_direito_acesso: "",
      outraforma_direito_acesso: "",
      medidas_fisicas_seguranca: "",
      medidas_logicas_seguranca: "",
      parecer_representante_trabalhadores: "",
    };
  },

  methods: {
    async onSubmit(values) {
      const datas = {
        tipo_notificacao: this.tipoNotificacao,
        tipo_pessoa: this.tipoPessoa,
        nome_denominacao: this.nome_denominacao,
        nome_comercial: this.nome_comercial,
        atividade_desenvolvida: this.atividadeDesenvolvida,
        numero_nif: this.numero_nif,
        rua_responsavel_tratamento: this.rua_responsavel_tratamento,
        local_responsavel_tratamento: this.local_responsavel_tratamento,
        ilha_responsavel_tratamento: this.ilhaResp,
        concelho_responsavel_tratamento: this.concelhoResp,
        caixapostal_responsavel_tratamento:
          this.caixapostal_responsavel_tratamento,
        telefone_responsavel_tratamento: this.telefone_responsavel_tratamento,
        email_responsavel_tratamento: this.email_responsavel_tratamento,
        pais_responsavel_tratamento: this.pais_responsavel_tratamento,
        nome_representante_instalacao: this.nome_representante_instalacao,
        rua_representante_instalacao: this.rua_representante_instalacao,
        caixapostal_representante_instalacao:
          this.caixapostal_representante_instalacao,
        local_representante_instalacao: this.local_representante_instalacao,
        ilha_representante_instalacao: this.ilhaMorRep,
        concelho_representante_instalacao: this.concelhoMorRep,
        nome_pessoa_contato_representante_instalacao:
          this.nome_pessoa_contato_representante_instalacao,
        email_pessoa_representante_instalacao:
          this.email_pessoa_representante_instalacao,
        contato_representante_instalacao: this.contato_representante_instalacao,
       // paisRep: this.paisRep,
        entidade_processamento_informacao:
          this.entidade_processamento_informacao,
        rua_processamento_informacao: this.rua_processamento_informacao,
        caixapostal_processamento_informacao:
          this.caixapostal_processamento_informacao,
        local_processamento_informacao: this.local_processamento_informacao,
        ilha_processamento_informacao: this.ilhaServExt,
        concelho_processamento_informacao: this.concelhoServExt,
        finalidadeTratamento: this.finalidade,
        categoriaDados: this.categoria,
        outrosDados: this.outrosDadosTratado,
        rua_direito_acesso: this.rua_direito_acesso,
        caixapostal_direito_acesso: this.caixapostal_direito_acesso,
        local_direito_acesso: this.local_direito_acesso,
        ilha_direito_acesso: this.ilhaDirAcess,
        concelho_direito_acesso: this.concelhoDirAcess,
        email_direito_acesso: this.email_direito_acesso,
        contato_direito_acesso: this.contato_direito_acesso,
        forma_direito_acesso: this.forma_direito_acesso,
        outraforma_direito_acesso: this.outraforma_direito_acesso,
        medidas_fisicas_seguranca: this.medidas_fisicas_seguranca,
        medidas_logicas_seguranca: this.medidas_logicas_seguranca,
        parecer_representante_trabalhadores:
          this.parecer_representante_trabalhadores,
      };
      //SUBMIT FORM WITH AXIOS
      axios.post("http://127.0.0.1:8000/api/geolocalizacao/create", datas, {
        headers: { "Content-Type": "multipart/form-data; charset=utf-8" },
      });
      console.log(values);
    },

    /*
    onSubmit(values) {
      console.log(values, null, 2);
      console.log("Clckado");
    },*/
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

    async dadosBackend() {
      const req = await fetch("http://localhost:3000/dadosBackend");
      const data = await req.json();
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
