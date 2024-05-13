<template>
  <div id="app" class="py-3">
    <header>
      <h1 class="text-center">Iniciando proyecto.</h1>
    </header>

    <main class="container">
      <section class="row justify-content-center g-3">
        <div
          class="col-12 col-md-6 col-lg-4"
          v-for="producto in productos"
          :key="producto.id"
        >
          <div class="card">
            <img
              :src="producto.pathImg"
              class="card-img-top"
              :alt="producto.nombre"
            />
            <div class="card-body">
              <h5 class="card-title">{{ producto.nombre }}</h5>
              <p class="card-text">
                {{ producto.descripcionCorta }}
              </p>

              <div>
                <button
                  class="btn btn-primary"
                  data-bs-toggle="modal"
                  data-bs-target="#miModal"
                  :data-producto-id="producto.id"
                  @click="mostrar"
                >
                  Ver detalles
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Modal -->
    <div
      class="modal fade"
      id="miModal"
      tabindex="-1"
      aria-labelledby="miModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="miModalLabel">
              {{ currentProducto.nombre }}
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <img :src="currentProducto.pathImg" alt="" />
            <p>
              <span>Descripción: </span>{{ currentProducto.descripcionLarga }}
            </p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      productos: [
        {
          id: 1,
          nombre: "Producto 1",
          descripcionCorta: "Descripción 1",
          pathImg: "./img/zapatilla1.jpg",
          descripcionLarga:
            "zapatilla con caña, color: blanco con detalles en negro, talla: 35 a 42",
        },
        {
          id: 2,
          nombre: "Producto 2",
          descripcionCorta: "Descripción 2",
          pathImg: "./img/zapatilla2.jpg",
          descripcionLarga: "color: blaco con diseño en negro , talla: 36 a 42",
        },
        {
          id: 3,
          nombre: "Producto 3",
          descripcionCorta: "Descripción 3",
          pathImg: "./img/zapatilla3.jpg",
          descripcionLarga:
            "zapatilla con plataforma media, color: blaco, talla: 36 a 40",
        },
      ],
      currentProducto: {},
    };
  },
  methods: {
    mostrar: function (event) {
      let element = event.target;
      let productoId = element.dataset.productoId;

      //buscar elemento dentro del array de productos
      let foundProducto = this.productos.find(
        (producto) => producto.id == productoId
      );

      if (foundProducto) {
        this.currentProducto = foundProducto;
      } else {
        alert("Producto no encontrado.");
      }
    },
  },
};
</script>
<style>
</style>
