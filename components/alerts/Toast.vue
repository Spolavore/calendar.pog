<template>
    <div
         class="absolute top-5 right-0 w-96 h-24 bg-white border border-e-neutral-100 shadow-md flex items-center rounded-s slide-in-right"
    >
        <div 
            class="h-full w-3 rounded-s"
            :class="estiloToast"    
        >
        </div>
        <div class="w-full flex items-center justify-start ml-5 gap-4">
            <img :src="iconeToast" alt="Erro icon">
            <div>
                <h2 class="font-bold"> {{ tituloToast }} </h2>
                <span class="text-sm">{{ texto }}</span>
            </div>
        </div>
    </div>
</template>

<script setup>

import IconeErro from "~/public/icons/error-circle.svg"
import IconeSucesso from "~/public/icons/check-circle.svg"


const props = defineProps(['texto', 'status'])
const tituloToast = ref('');
const estiloToast = ref('');


onMounted(() => {
    estilizaToast();
})

const iconeToast = computed(() => {
  switch(props.status) {  // Remova .value
    case 'Erro':
      return IconeErro;
    case 'Sucesso':
        return IconeSucesso
  }
})

const estilizaToast = () => {
  switch (props.status) {  // Remova .value
    case 'Erro':
      tituloToast.value = 'Erro';
      estiloToast.value = 'bg-red-500';
      return;
    case 'Sucesso':
      tituloToast.value = 'Sucesso';
      estiloToast.value = 'bg-green-500';
      return;
  }
}


</script>