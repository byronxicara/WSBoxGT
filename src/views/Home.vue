<template>
  <div class="home">
    <section class="section">
      <div class="container">
        <span class="title"> Cotizador WSBoxGT </span>
        <br />
        <br />
        <div class="columns">
          <div class="column">
            <label class="label">$ Monto Producto</label>
            <div class="control">
              <p class="control has-icons-left has-icons-right">
                <input
                  class="input is-info"
                  id="precio"
                  type="$MontoUS"
                  placeholder="Ingresa el monto del producto."
                  v-model="precio"
                />
              </p>
            </div>
          </div>
          <div class="column">
            <label class="label"> Peso del producto </label>
            <div class="control">
              <p class="control has-icons-left has-icons-right">
                <input
                  class="input is-info"
                  id="peso"
                  type="peso"
                  placeholder="Ingresa el peso del producto"
                  v-model="peso"
                />
              </p>
            </div>
          </div>
        </div>
        <div class="columns">
          <div class="column">
            <label class="label">Shipping del producto</label>
            <div class="control">
              <p class="control has-icons-left has-icons-right">
                <input
                  class="input is-info"
                  id="shipping"
                  type="$MontoUS"
                  placeholder="Ingresa el monto del producto."
                />
              </p>
            </div>
          </div>
          <div class="column">
            <label class="label">Selecciona la descripcion del producto</label>
            <div class="select is-primary is-flex-direction-column">              
              <select v-model="selected">
                <option
                  v-for="daiValue in daiValues"
                  :key="daiValue"
                  :value="daiValue.value"
                >
                  {{ daiValue.description }}
                </option>
              </select>
            </div>
          </div>
        </div>
        <div class="columns">
          <div class="column">
            <span class="is-flex is-justify-content-flex-start"
              >Precio del envio Q{{totalCalculado}}</span
            >
            <br />
            <span class="is-flex is-justify-content-flex-start"
              >Envio al departamento Q{{ 40 }}</span
            >
            <br>
            <button @click="calculo" type="submit" class="button is-success is-light">Calculo</button>
          </div>
          <div class="column">
            <span class="is-flex is-justify-content-flex-start"
              >Nuestra Ganancia Q Byron: {{ ganancia }} chaquilin: {{ ganancia}}</span
            >                      
            <br>
            <span class="is-flex is-justify-content-flex-start title is-2">
              Total con Ganancia Q.{{totalConGanancia}}
            </span>                
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
  data() {
    return {
      precio: 0,
      peso: 0,      
      tipoCambio:7.86,
      costoPorLibra:3.4,
      desaduanaje:4.5,
      totalCalculado:0,
      totalConGanancia:0,
      ganancia:0,
      daiValues: [
        { value: 15, description: "Accesorio de Cámara" },
        { value: 15, description: "Accesorio de Carro" },
        { value: 15, description: "Accesorio de Cocina" },
        { value: 15, description: "Accesorio de Computacion" },
        { value: 15, description: "Accesorio de Musica" },
        { value: 15, description: "Accesorio de Oficina" },
        { value: 15, description: "Accesorio de Telefonia" },
        { value: 15, description: "Accesorio Deportivo" },
        { value: 0, description: "Accesorio Electrico" },
        { value: 15, description: "Articulos de Cuero" },
        { value: 15, description: "Articulos de Fiesta" },
        { value: 15, description: "Bateria de Carro" },
        { value: 15, description: "Bicicleta" },
        { value: 0, description: "Bocinas de Carro" },
        { value: 15, description: "Bolsas" },
        { value: 10, description: "Cables" },
        { value: 0, description: "Camara Fotografica" },
        { value: 10, description: "Cartucho de tinta (Simple)" },
        { value: 0, description: "Cartucho de Tinta C/Chip" },
        { value: 15, description: "Catalogos" },
        { value: 13, description: "CD´s" },
        { value: 0, description: "Celulares" },
        { value: 5, description: "Cinta de Impresora" },
        { value: 0, description: "Computadoras" },
        { value: 15, description: "Consola de Videojuegos" },
        { value: 15, description: "Cosmeticos" },
        { value: 15, description: "Cuadernos" },
        { value: 0, description: "Discos Duros Vacios" },
        { value: 18, description: "DVD Player" },
        { value: 15, description: "Edredon" },
        { value: 15, description: "Electrodomesticos" },
        { value: 0, description: "Equipo Medico" },
        { value: 15, description: "Estuche de Cuero" },
        { value: 15, description: "Estuche Partes Plasticas" },
        { value: 15, description: "Etiquetas de Papel o Carton" },
        { value: 15, description: "Etiquetas de Tela" },
        { value: 15, description: "Grabadoras" },
        { value: 0, description: "Herramientas de Mano" },
        { value: 0, description: "Impresoras" },
        { value: 15, description: "Joyeria/Bisuteria" },
        { value: 15, description: "Juguetes" },
        { value: 0, description: "Laptop" },
        { value: 15, description: "Lentes" },
        { value: 0, description: "Lentes (solo aro)" },
        { value: 5, description: "Lentes de Contacto" },
        { value: 15, description: "Lentes de Sol" },
        { value: 0, description: "Libros" },
        { value: 5, description: "Llaves" },
        { value: 15, description: "Luces Navideñas" },
        { value: 15, description: "Mascarillas" },
        { value: 15, description: "Material Impreso" },
        { value: 15, description: "Material Promocional" },
        { value: 15, description: "Medicamentos" },
        { value: 15, description: "MP3 (iPod)" },
        { value: 15, description: "Muebles de Casa" },
        { value: 10, description: "Partes de Bicicleta" },
        { value: 10, description: "Partes Industriales" },
        { value: 15, description: "Poster" },
        { value: 15, description: "Radio de Carro" },
        { value: 15, description: "Reloj de Pulsera/Pared" },
        { value: 10, description: "Repuestos de Carro" },
        { value: 0, description: "Repuestos de Helicoptero" },
        { value: 0, description: "Repuestos de Motor de Carro" },
        { value: 0, description: "Repuestos Electronicos" },
        { value: 15, description: "Ropa" },
        { value: 0, description: "Scanner" },
        { value: 0, description: "Software de PC" },
        { value: 0, description: "Tablets (iPad)" },
        { value: 15, description: "Tarjetas de Invitaciones" },
        { value: 0, description: "Videocamara" },
        { value: 18, description: "Videocintas" },
        { value: 3, description: "Videojuegos CD/DVD/BlueRay-" },
        { value: 18, description: "Videojuegos Cassette" },
        { value: 15, description: "Zapatos" },
      ],
    };
  },
  methods:{
      calculo(){    
        let nuevoPrecio = this.precio * 1.07    
        let dai = ((nuevoPrecio) * (0.15+(this.selected / 100))) 
        let servicio =(this.peso * this.costoPorLibra) + this.desaduanaje
        let montoSinGanancia = ((nuevoPrecio* this.tipoCambio) + (dai * this.tipoCambio)) + (servicio* this.tipoCambio)
        this.totalCalculado = montoSinGanancia.toFixed(2)               
      this.totalConGanancia = ((montoSinGanancia * 1.12)).toFixed(2)      
      this.ganancia = ((montoSinGanancia * 0.12)/2).toFixed(2)
      },      
  },
};
</script>
