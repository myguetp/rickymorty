<script>
export default {
    

 data: function() {
    return {
      el:'#perso',
      personajes :  [],
      texto:'',
      //arrayfiltrado: []
     

    };
  },

  methods: {
    formatDate : (fecha) => {
        let date = new Date(fecha)
        let day = `${(date.getDate())}`.padStart(2,'0');
        let month = `${(date.getMonth()+1)}`.padStart(2,'0');
        let year = date.getFullYear();
        
        return `${day}/${month}/${year}`
    }
 
  },
  
  


  computed: {
    filtro:{
        get(){
            return this.texto;
        },
        set(value){
            console.log(value)
            value = value.toLowerCase();
            this.personajes = this.personajes.filter(item =>
                item.name.toLowerCase().indexOf(value) !== -1
            )       

            this.texto = value;
           
        }
          

    },

  },

  created(){
    this.personajes;
    this.arrayfiltrado = this.personajes;
  },
  mounted() {
    fetch("https://rickandmortyapi.com/api/character")
    .then(res => res.json())
    .then(data => (
       data = data.results,
       this.personajes = data,
       data = data.results.origin,
       this.personajes = data,
       data = data.results.created

    ))
    .catch(error => console.log(error))   

  },
  
};
</script>


<template>
    
    <section>

    <div class="filtros">
        <img class="perso" src="../assets/img/camera-movie.png" alt="camera">
        <h2 class="perso" >Personajes</h2>
    </div>

    <div class="contenedor">
        <div class="flitrosperso tp" >
            <p class="tperson">Total de Personajes</p>
            <p class="tperson">{{personajes.length}}</p>
        </div>
         <div class="flitrosperso pv" >
            <img class="pvivos" src="../assets/img/Icono de vivo.png" alt="camera">
            <p class="pvivos" >Personajes vivos</p>
            <p class="pvivos" >8</p>
            
        </div>
         <div class="flitrosperso pm" > 
            <img class="pmuertos" src="../assets/img/Icono de muerto.png" alt="camera">
            <p class="pmuertos">Personajes muertos</p>
            <p class="pvivos" >6</p>
        </div>

        <input class="flitrosperso pm" placeholder="Buscar" v-model="filtro">
                
    </div>
    
    

   
            <div class="alltable">         
                 <table class="table" id="perso">
                    <thead class="cabecera">
                    <tr class="cabecera">
                        <th>Nombre</th>
                        <th>Vivo</th>
                        <th>Especie</th>
                        <th>Genero</th>
                        <th>Origen</th>
                        <th>Locación</th>
                        <th>Capitulos</th>
                        <th>Fecha</th>
                        <th>Acciones</th>
                    </tr>
                    </thead>
                    <tbody class="bodye"> 
                        <tr class="bodye" v-for="i in personajes">
                        <td>{{i.name}}</td>
                        <td>
                         <span v-if="i.status == 'Alive'">
                            <img src="../assets/img/Icono de vivo.png" >
                         </span>
                           <span v-if="i.status == 'Dead'">
                            <img src="../assets/img/Icono de muerto.png" >
                         </span>
                        
                        </td>
                        <td>{{i.species}}</td>
                        <td>{{i.gender}}</td>
                        <td>{{i.origin.name}}</td>
                        <td>{{i.location.name}}</td>
                        <td>{{i.episode.length}}</td>
                        <td>{{formatDate(i.created)}}</td>
                        <td>                           
                            <div>
                                <img :src="i.image" alt="personaje" class="laimg">
                            </div>
                        </td>
                        </tr>

                       
                    </tbody>
                    </table>
              </div>
    </section>      


   

</template>

<style scoped>
.filtros{
    margin-top: 24px;
    margin-left: 32px;
    margin-bottom: 24px;
    
}

.perso{
    border: none;
    display: inline-block; 
}

.flitrosperso{
    display: inline-block; 
    border: 2px solid lightgray;
    margin-left:20px;

}

.tp{
    margin-left:32px;
    width: 250px;
    padding: auto;
    font-weight: bold;  
    border-radius: 5px
}
.pv{
    margin-left:32px;
    width: 250px;
    width: 250px;
      font-weight: bold;  
    border-radius: 5px
}

.pm{
    margin-left:32px;
    width: 250px;
    width: 250px;
      font-weight: bold;  
    border-radius: 5px
}

h2{

    color: #10454f;
    font-weight: bold;
    font-size: 34px
}




.cabecera{
  background-color: #506266;
  padding:15px;
 
  color: #fff;
  margin-top: 24px;
  padding:15px;

}
.tperson{
    display:inline-block;   
    margin-left:10px;
    font-weight: bold;
}
.pvivos{
    display:inline-block;   
    margin-left:10px;
    font-weight: bold; 
}

.pmuertos{
    display:inline-block;
    margin-left:10px;
    font-weight: bold; 
}

table{
    

    border: 2px solid lightgray;
    padding:24px;
    width: calc(100%-2rem);
    border-radius: 5px;
    box-sizing: border-box;
    margin: 1rem;
   
}

.bodye{
    margin-top: 16px;
}

.alltable{
 
    border: 2px solid lightgray;
    padding:24px;
    width: calc(100%-2rem);
    border-radius: 5px;
    box-sizing: border-box;
    margin: 1rem;
}

.laimg{
    width:15px
}

.laimg:hover{
    width:100px
}

</style>