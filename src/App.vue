<script setup>
import { ref } from "vue";

const img = ref({
  dado: "",
  error: false,
});

async function trazDados() {
  const resp = await fetch(`https://dog.ceo/api/breeds/image/random`);
  const data = await resp.json();

  img.value.dado = {
    doguinho: data.message,
  };
  console.log(data);

  if (data.status == "error") {
    img.value.error = true;
  }
}
</script>

<template>
  <div class="conteiner">
    <div class="titulo">
      <p>Melhore o seu dia clicando no botão <3!</p>
    </div>
    <div class="botao">
      <button class="btn" @click="trazDados">Clique-me</button>
    </div>

    <div v-if="!img.error" class="dog">
      <img

        :src="img.dado.doguinho"
        alt="O doguinho irá aparecer aqui"
      />
    </div>

    <div class="error">
      <p v-if="img.error" class="erro">
        Desculpe, não foi possível exibir a imagem!
      </p>
    </div>
  </div>
</template>

<style scoped>

</style>
