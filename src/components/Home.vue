<template>
    <div class="home">
      <!-- {{msg}} -->
      <div>
        <h1 class="title">Ciudades</h1>
        
  
        <div class="container">
          <div class="row">
            <div class="card productos" @click="" v-for="product in products" :key="product.id" track-by="id">
              <div class="card-body">
                <img :src="product.img" :alt="`imagen ${product.ciudad}`" class="card-img-top" />
                <h5 class="card-title">
                  <p>{{product.ciudad}}</p>
                </h5>
                <hr>

                <div class="" v-for="establecimientos in orderedStars( product.establecimientos)" :key="establecimientos.id" track-by="establecimientos.id">
                    <h4>Establecimiento: {{establecimientos.id}}</h4>
                    <p style="color=white">Direccion: {{establecimientos.direccion}}</p>
                    <p style="color=white">Nombre: {{establecimientos.nombre}}</p>
                    <!-- <p style="color=white">{{establecimientos.id}}</p> -->
                    <!-- <p style="color=white">{{establecimientos.fotografias}}</p> -->
                    <p style="color=white">Calificacion:{{establecimientos.estrellas}}</p>

                    <div class="card" v-for="(menus, key) in establecimientos.menu"  track-by="id">
                        {{key}} {{menus.plato}} - {{menus.precio}}
                    </div>
                    <div>
                        Califique el menu: 
                        <input type="text" v-model="estab">
                        <button @click="califica(establecimientos.estrellas)">
                            califique
                        </button>
                    </div>

                    <hr>
                </div>

              </div>
            </div>
          
        
        
        
          </div>
        </div>
      
      </div>
    </div>
  </template>
  
  <script>
  import { mapGetters, mapActions } from 'vuex'
  export default {
    
    created(){
      this.fetchDataciudades();
    },
    name: 'Home',
    props: {
      mm: Number
    },
    data: function(){
        return{
            estab: 0
        }
    },
    computed: 
    {
     ...mapGetters({
            products: 'allProducts',
            length: 'getNumberOfProducts'
        })
    },
    methods:{
        orderedStars: function (esta) {
            return _.orderBy(esta, 'estrellas', 'desc')
        },
        ...mapActions([
            'addToCart', 'restToCart', 'fetchData', 'fetchDataciudades'
        ]),
        ir(p){
            this.$router.push({ path: '/detalle/'+ p.id })
        },
        califica(esta){
            esta = this.estab;
        }
    }
  }
  </script>
  
  
  
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  .productos{
    position: relative;
    width: 30%;
    padding: 5em;
    background-color: black;
    color: white;
    display: inline-flex;
    margin: 1em;
  }
  </style>
  