<template>
  <div
    class="w-screen h-screen flex items-center justify-center"
  >
    <div class="flex flex-col gap-5 items-center justify-center p-[200px]">
      <img src="/images/logo-poggers.webp" class="w-20 h-20"> 
      <span class="text-2xl font-bold"
        >Bem vindo ao <span class="text-green-500">Calendar.pog</span></span
      >
      <input class="input-padrao" placeholder="Digite seu email" v-model="email" />
      <div class="flex w-full gap-2">
        <input class="input-padrao" :type="visibilidadeSenha" placeholder="Digite sua senha" v-model="senha" />
        <img v-if="senha" class="cursor-pointer svg-azul-500" @click="() => senhaVisivel = !senhaVisivel" :src="IconeVisibilidade" />
      </div>
      <div class="flex flex-row-reverse gap-3 w-full">
        <button class="bg-blue-600 text-white hover:bg-blue-700 button">Logar</button>
        <button class="text-neutral-400 hover:bg-gray-100 button" @click="() => navigateTo({path: 'cadastrar-usuario'})">Cadastrar</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const email = ref("");
const senha = ref("");
const senhaBackup = ref("senha")
const senhaVisivel = ref(false);

// Computed Properties
const IconeVisibilidade = computed(() => {
  return senhaVisivel.value ? "/icons/visibility.svg" : "/icons/visibility_off.svg"
});

const visibilidadeSenha = computed(() => { 
  return senhaVisivel.value ? 'text' : 'password';
})

</script>

<style scoped>
.button {
  @apply py-1 px-4 rounded font-semibold
}
</style>
