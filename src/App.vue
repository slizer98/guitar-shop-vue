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
  const guitarra = ref({})


  onMounted(() => {
    // state.guitarras = db
    guitarras.value = db;
    guitarra.value = db[3];
  })

  const agregarCarrito = (guitarra) => {
    const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id);

    if(existeCarrito  >= 0) {
      carrito.value[existeCarrito].cantidad++;
    } else {
      guitarra.cantidad = 1;
      carrito.value.push(guitarra);
    }
  }


  const decrementarCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id);
    if(carrito.value[index].cantidad === 1) return;
    carrito.value[index].cantidad--
  } 

  const incrementarCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id);
    carrito.value[index].cantidad++
  }  

  const eliminarProducto = (id) => {
    carrito.value = carrito.value.filter(producto => producto.id !== id);
  } 

  const vaciarCarrito = () => {
    carrito.value = [];
  }
  
</script>

<template>
  <Header 
    :carrito="carrito" 
    :guitarra="guitarra"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @eliminar-producto="eliminarProducto"
    @vaciar-carrito="vaciarCarrito"
    @agregar-carrito="agregarCarrito"
  />
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
