<script setup>
  import { ref, reactive, onMounted } from 'vue';
  import { db } from './data/guitarras'
  import { Header, Guitarra, Footer  } from './components'

  // const state = reactive({
  //   guitarras: []
  // })
  // console.log(state.guitarras)

  const guitarras = ref([])
  const carrito = ref([])


  onMounted(() => {
    // state.guitarras = db
    guitarras.value = db
  })

  const agregarCarrito = (guitarra) => {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra);
  }
  
</script>

<template>
  <Header :carrito="carrito" />
  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <Guitarra
        v-for="guitarra in guitarras"
        :guitarra="guitarra"
        @agregar-carrito="agregarCarrito"
       />
    </div>
  </main>
  <Footer />  
</template>
