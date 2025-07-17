<template>
  <v-container class="fill-height" fluid style="background-color: #363636;">
    <v-row align="center" justify="center">
      <v-col cols="12" sm="8" md="4">

        <v-card theme="dark" class="mx-auto pa-4" max-width="400">
          
          <v-card-title class="text-h5 font-weight-bold mb-5">
            Login
          </v-card-title>

          <v-card-text>
            <v-form ref="form" @submit.prevent="handleLogin">
              
              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
                variant="filled"
                class="mb-4"
              ></v-text-field>

              <v-text-field
                v-model="password"
                :rules="passwordRules"
                label="Senha"
                variant="filled"
                type="password"
              ></v-text-field>
              
              <v-btn
                :loading="loading"
                type="submit"
                block
                color="blue"
                size="large"
                class="mt-8 mb-4"
              >
                ENTRAR
              </v-btn>

            </v-form>
            
            <v-btn
              block
              variant="text"
            >
              CRIAR CONTA
            </v-btn>

          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from 'vue';

const form = ref(null); 

const email = ref('');
const password = ref('');

const loading = ref(false);


const emailRules = [
  value => !!value || 'Campo obrigatório',
  value => /.+@.+\..+/.test(value) || 'E-mail deve ser válido.',
];

const passwordRules = [
  value => !!value || 'Campo obrigatório',
];

async function handleLogin() {
  const { valid } = await form.value.validate();

  if (valid) {
    loading.value = true;
    setTimeout(() => {
      loading.value = false;
      console.log('Login com:', email.value);
      alert('Login efetuado com sucesso!');
    }, 2000); 
  }
}
</script>