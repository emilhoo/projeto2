<template>
  <v-container class="fill-height" fluid style="background-color: #363636;">
    <v-row align="center" justify="center">
      <v-col cols="12" sm="8" md="6">
        <v-card theme="dark" class="mx-auto pa-4" max-width="700">
          <v-card-title class="text-h5 font-weight-bold mb-5">
            Cadastro de Banco
          </v-card-title>

          <v-card-text>
            <v-form ref="form" @submit.prevent="salvar">
              <v-text-field
                v-model="banco.numero"
                :rules="regraCampoObrigatorio"
                label="Número do Banco"
                variant="filled"
                class="mb-4"
              ></v-text-field>

              <v-text-field
                v-model="banco.descricao"
                :rules="regraCampoObrigatorio"
                label="Descrição do Banco"
                variant="filled"
                class="mb-4"
              ></v-text-field>

              <v-switch
                v-model="banco.ativo"
                label="Banco Ativo?"
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
                SALVAR
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

const banco = reactive({
  numero: '',
  descricao: '',
  ativo: true,
});

const regraCampoObrigatorio = [
  value => !!value || 'Este campo é obrigatório.',
];

async function salvar() {
  const { valid } = await form.value.validate();

  if (valid) {
    loading.value = true;
    console.log('Dados a serem salvos:', banco);

    setTimeout(() => {
      loading.value = false;
      alert('Banco salvo com sucesso!');
      form.value.reset();
      banco.ativo = true;
    }, 1500);
  } else {
    console.log('Formulário inválido.');
  }
}
</script>

<style scoped>
/* Estilos específicos para esta página, se necessário */
</style>