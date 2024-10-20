<template>
  <div class="flex flex-col justify-center items-center w-screen h-screen">
    <div class="flex flex-col items-center justify-center">
      <img :src="Logo" class="w-20 h-20" />
      <h1 class="text-xl font-bold">
        Primeiro acesso <span class="text-green-500">aqui</span> ?
      </h1>
      <span class="text-lg mb-10"
        >Preencha as informação abaixo para se cadastrar</span
      >

     <label class="label-column">
          Email
         <input placeholder="" id="email" class="input-padrao" />
     </label>
     <label class="label-column">
          Senha
         <input placeholder="" id="email" class="input-padrao" />
     </label>
     <label class="label-column">
          Confirmar senha
         <input placeholder="" id="email" class="input-padrao" />
     </label>
      <input class="" />
    </div>
  </div>
</template>

<script setup>
import Logo from "@/assets/images/logo-poggers.webp";

onMounted(() => {
  console.log("oiii");
});
</script>


<style scoped>

.label-column {
    @apply flex flex-col gap-1 w-full mb-4
}

</style>
