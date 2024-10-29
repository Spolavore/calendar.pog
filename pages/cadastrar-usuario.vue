<template>
  <div
    v-if="true"
    class="w-screen h-screen bg-white flex items-center justify-center"
  >
  <NuxtImg 
    width="250"
    src="/images/email-verificacao.png"
    />
  </div>
  <div 
    v-else
    class="flex flex-col justify-center items-center w-screen h-screen">
    <div class="flex flex-col items-center justify-center">
      <img src="/images/logo-poggers.webp" class="w-20 h-20" />
      <h1 class="text-xl font-bold">
        Primeiro acesso <span class="text-green-500">aqui</span> ?
      </h1>
      <span class="text-lg mb-10"
        >Preencha as informação abaixo para se cadastrar</span
      >

    <form class="w-full" @submit.prevent="submitCadastroUsuario">
      <label class="label-column">
          Nome
         <input v-model="nome" placeholder=""  class="input-padrao" required />
     </label>
     <label class="label-column">
          Email
         <input v-model="email" placeholder="" type="email" class="input-padrao" required />
     </label>
     <label class="label-column">
          Senha
         <input v-model="senha" placeholder="" :type="visibilidadeSenha" class="input-padrao" required />
     </label>
     <label class="label-column">
          Confirmar senha
         <input v-model="senhaConfirmacao" :type="visibilidadeSenha" placeholder="" class="input-padrao" required />
     </label>
     <label class="label-column">
          32 + 37?
         <input v-model="resVerificacao"  placeholder=""  class="input-padrao" required />
     </label>
     <div class="flex w-full justify-end gap-4">
       <button class="text-neutral-400 hover:bg-gray-100 button" @click="() => navigateTo({path: 'login'})">Voltar</button>
       <button class="bg-blue-600 text-white hover:bg-blue-700 button">Cadastrar</button>
     </div>
    </form>
    </div>
    <Toast v-if="mostrarToast" :texto="textoToast" :status="tipoToast"/>
  </div>
</template>

<script setup>

import Toast from '~/components/alerts/Toast.vue';
import RequestService from '~/services/RequestService';
import api from "~/utils/Constants";

const nome = ref('');
const email = ref('');
const senha = ref('');
const senhaConfirmacao = ref('');
const resVerificacao = ref('');
const senhaVisivel = ref(false);
const textoToast = ref('');
const mostrarToast = ref(false);
const tipoToast = ref('');
const showVerificarEmail = ref(false);

const visibilidadeSenha = computed(() => {
  return senhaVisivel.value ? 'text' : 'password'
});

const submitCadastroUsuario = async () => {
  if(!(senha.value === senhaConfirmacao.value)){
    tipoToast.value = 'Erro'
    textoToast.value = ('As senhas informadas não são iguais!');
    mostrarToast.value = true;
  }
  else if(resVerificacao.value != 69){   
    tipoToast.value = 'Erro'
    textoToast.value = ('Oops, parace que você errou uma soma basica.');
    mostrarToast.value = true;
  }
  else {
    await cadastrarUsuario();  
  }
}

const cadastrarUsuario = async () => {
  const options = {
    url: api.cadastrar_usuario,
    data: {
      nome: nome.value,
      email: email.value,
      senha: senha.value
    },
    callback: () => {
      resetarCampos();
      showVerificarEmail.value = true;
    },
    errorCallback: (error) => {
      console.error(error);
    }
  }
  await RequestService.postRequest(options);
}

const resetarCampos = () => {
   nome.value = ''
   email.value = ''
   senha.value = ''
   senhaConfirmacao.value = ''
   resVerificacao.value = ''
}

</script>


<style scoped>

.label-column {
    @apply flex flex-col gap-1 w-full mb-4
}

</style>
