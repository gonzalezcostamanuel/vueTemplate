

<!-- ******************************************************************************* -->
<!--                                                                                 -->
<!--                                HTML CODE SECTION                                -->
<!--                                                                                 -->
<!-- ******************************************************************************* -->


<template>
  <v-app class="main">
    <div class="mainContainer">
      <v-row class="justify-center">
        <h1>Title</h1>
      </v-row>
    </div>
    <footer>
      <p>Vue example footer</p>
    </footer>
  </v-app>
</template>


<!-- ******************************************************************************* -->
<!--                                                                                 -->
<!--                             JavaScript CODE SECTION                             -->
<!--                                                                                 -->
<!-- ******************************************************************************* -->

<script>
/***************************************************************************/
/*                   Imports necesarios en este componente                 */
/***************************************************************************/
import mixin from "src/mixins/mixin.vue";
import Component from "src/components/Component.vue";

export default {

    /***************************************************************************/
    /*                         Nombre del componente                           */
    /***************************************************************************/
    name: "NombreComponente",

    /***************************************************************************/
    /*                    Mixins que tiene el componente                       */
    /***************************************************************************/
    mixins: [mixin],

    /***************************************************************************/
    /*                   Componentes que usa este componente                   */
    /***************************************************************************/
    components: {
        Component
    },

    /***************************************************************************/
    /*      Propiedades del componente que le son pasadas desde el padre       */
    /***************************************************************************/
    props: {
        reload: {
            type: Boolean,
            default: false
        }
    },

    /***************************************************************************/
    /*                 Variables utilizadas en este componente                 */
    /***************************************************************************/
    data: () => ({

        //Array 
        someArray: [],

        //Boolean
        isLoading: true,

        //Strings
        firstName: "Manuel",
        lastName: "Gonzalez"
    }),


    /***************************************************************************/
    /*        Cada computed que creemos será como una variable                 */
    /*           que tiene el valor que definamos (siempre actualizado).       */
    /*           Es decir, si cambia firstName cambiará automáticamente        */
    /*           el valor de fullName donde lo estemos utilizando              */
    /***************************************************************************/
    computed: {
      fullName: function () {
        return this.firstName + ' ' + this.lastName
      }
    },

    /***************************************************************************/
    /*       Acciones que se realizan cuando es creado este componente         */
    /*                                                                         */
    /*  Cuando este método es ejecutado el DOM aún no esá accesible
        pero sí lo están los datos con su reactividad.
        Es una buena opción para utilizar cuando queremos inicializar datos    */
    /***************************************************************************/
    created: async function () {
        this.isLoading = true; //Mostramos ventana carga
        this.someArray = await this.getData(); //Obtenemos datos
        this.isLoading = false; //Cerramos ventana carga
    },

    
    /***************************************************************************/
    /*   Acciones que se realizan cuando el componente ya tiene el DOM listo   */
    /*                                                                         */
    /*  Cuando este método es ejecutado el DOM justo acaba de ser montado,
        por lo que ya podemos empezar a modificar sus elementos                */
    /***************************************************************************/
    mounted: function() {
        //Javascript code
    },

    /***************************************************************************/
    /*              Métodos que monitorizan el valor de una variable y         */
    /*                    realizan una acción cuando éste cambia.              */
    /***************************************************************************/
    watch: {
        reload: async function (esTrue) {
            //Cuando el padre varía el valor de reload y lo pone a true se ejecuta este código
            if (esTrue) {

                this.isLoading = true;

                this.someArray = await this.getData();
                
                this.isLoading = false;

                this.$emit("reloaded"); //Se lanza una señal al padre
            }

        }
    },

    /***************************************************************************/
    /*          Declaración de los métodos locales a este componente           */
    /***************************************************************************/
    methods: {
        myFunction(p1, p2) {
          return p1 * p2;   // The function returns the product of p1 and p2
        },
    },


};
</script>



<!-- ******************************************************************************* -->
<!--                                                                                 -->
<!--                                  CSS CODE SECTION                               -->
<!--                                                                                 -->
<!-- ******************************************************************************* -->
<!--                                                                                 -->
<!--       Si no utilizamos scoped afectaría a otros componentes de la app           -->
<!-- ******************************************************************************* -->

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  overflow: auto;
}

.main {
  width: 100vw;
}

footer {
  height: 60px;
  margin-bottom: 20px;
}


</style>
