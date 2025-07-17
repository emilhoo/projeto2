<template>
  <v-container class="fill-height" fluid style="background-color: #363636;">
    <v-row align="center" justify="center">
      <v-col cols="12" sm="10" md="8" lg="7">
        <v-card theme="dark" class="mx-auto pa-4">
          <v-card-title class="text-h5 font-weight-bold mb-5">
            Cadastro de Conta Bancária
          </v-card-title>

          <v-card-text>
            <v-form ref="form" @submit.prevent="salvar">
              <v-row>
                <v-col cols="12" md="6">
                  <v-select
                    v-model="conta.bancoId"
                    :items="bancos"
                    item-title="nome"
                    item-value="id"
                    label="Banco"
                    variant="filled"
                    :rules="regraCampoObrigatorio"
                  ></v-select>
                </v-col>
                <v-col cols="12" md="3">
                  <v-text-field
                    v-model="conta.agencia"
                    label="Agência"
                    variant="filled"
                    :rules="regraCampoObrigatorio"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" md="3">
                   <v-text-field
                    v-model="conta.agenciaDigito"
                    label="Dígito da Agência"
                    variant="filled"
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row>
                <v-col cols="12" md="9">
                  <v-text-field
                    v-model="conta.numero"
                    label="Número da Conta"
                    variant="filled"
                    :rules="regraCampoObrigatorio"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" md="3">
                  <v-text-field
                    v-model="conta.numeroDigito"
                    label="Dígito da Conta"
                    variant="filled"
                  ></v-text-field>
                </v-col>
              </v-row>

               <v-text-field
                v-model="conta.saldoInicial"
                label="Saldo Inicial"
                variant="filled"
                type="number"
                prefix="R$"
                :rules="regraCampoObrigatorio"
              ></v-text-field>
              
              <v-text-field
                v-model="conta.dataCriacao"
                label="Data de Criação da Conta"
                variant="filled"
                placeholder="dd/mm/aaaa"
                :rules="regraCampoObrigatorio"
              ></v-text-field>

              <v-switch
                v-model="conta.ativa"
                label="Conta Ativa"
                color="blue"
                inset
              ></v-switch>

              <v-btn
                :loading="loading"
                type="submit"
                block
                color="blue"
                size="large"
                class="mt-6"
              >
                SALVAR CONTA
              </v-btn>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, reactive } from 'vue';

const form = ref(null);
const loading = ref(false);

const conta = reactive({
  bancoId: null,
  agencia: '',
  agenciaDigito: '',
  numero: '',
  numeroDigito: '',
  saldoInicial: 0.00,
  dataCriacao: null,
  ativa: true, 
});

const bancos = ref([
  { id: 1, nome: 'Banco do Brasil' },
  { id: 2, nome: 'Santander' },
  { id: 3, nome: 'Caixa Econômica Federal' },
  { id: 4, nome: 'Itaú' },
  { id: 5, nome: 'Bradesco' },
]);

const regraCampoObrigatorio = [
  value => !!value || 'Este campo é obrigatório.',
];

const regraSaldoNaoNegativo = [
  value => value >= 0 || 'O saldo não pode ser negativo.',
];

async function salvar() {
  const { valid } = await form.value.validate();

  if (valid) {
    loading.value = true;
    console.log('Dados da conta a serem salvos:', conta);

    setTimeout(() => {
      loading.value = false;
      alert('Conta salva com sucesso!');
      form.value.reset(); 
      conta.ativa = true; 
    }, 2000);
  } else {
    console.log('Formulário inválido. Verifique os campos.');
  }
}
</script>

<style scoped>
</style>