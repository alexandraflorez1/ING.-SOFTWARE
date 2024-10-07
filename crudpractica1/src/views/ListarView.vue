<template>

  <div class="container"> 
    <div class="input-group mb-3">
    <span class="input-group-text"  id="inputGroup-sizing-default">Documento </span>
    <input v-model= "docBuscar" type="text" placeholder="Ingrese el documento" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
    <button 
    class="btn btn-primary" 
    type="button"
    id="inputGroup-sizing-default"
    @click="BuscarPaciente(docBuscar)"
    >Buscar</button>
  </div>
    
    <div class="card"> 
      <div class="card-header">
        <h1>LISTA DE PACIENTES</h1>
      </div>
      <div class="card-body">
        <div
          class="table-responsive"
        >
          <table
            class="table table-primary"
          >
            <thead>
              <tr>
                <th scope="col">ID</th>
                <th scope="col">Documento</th>
                <th scope="col">Nombres</th>
                <th scope="col">Apellidos</th>
                <th scope="col">   </th>

              </tr>
            </thead>
            <tbody>
              <tr  v-for="paciente in Pacientes" v-bind:key="paciente.id">
                  <td scope="row">{{ paciente.id }}</td>
                  <td>{{ paciente.Doc }}</td>
                  <td>{{ paciente.Nombre }}</td>        
                  <td>{{ paciente.Apellido }}</td>   
                  <td>
                    <div class="btn-group" role="group" aria-label="Button group name">
                      <button
                        type="button"
                        class="btn btn-primary"
                      >
                        Ver resultados
                      </button>
                     
                      <router-link :to="{ name: 'editar', params: { id: paciente.id } }" class="btn btn-primary">Editar</router-link>

                      <button
                        type="button"
                        class="btn btn-danger"
                        @click="eliminarPaciente(paciente.id)"

                      >
                        Eliminar
                      </button>
                    </div>
                    
                  </td>

              </tr>
            </tbody>
          </table>
        </div>
        
      
      </div>
      
    </div>
  </div>
  </template>
  
  <script>

export default {
  data(){
    return{ 
    Pacientes:[],
    pacienteEncontrado:[], // Para almacenar los datos del paciente si se encuentra
    mensajeError: '', // Mensaje de error en caso de fallo o paciente no encontrado
  }
  },
  

    created:function(){
      this.consultarPacientes(); 
    },

    methods:{
      consultarPacientes(){
         fetch('http://localhost/API/')
        .then(response => response.json())
        .then((data)=>{
          console.log(data)
          this.Pacientes=[];
          if(typeof data[0].sucess==='undefined'){
          this.Pacientes=data
        }
        
        })
        .catch(console.log)
      },

      eliminarPaciente(id){
        console.log(id);
        fetch('http://localhost/API/?borrar='+id)
          .then(response=>response.json())
          .then((data)=>{
            console.log(data)
            window.location.href='listar'
        })
        .catch(console.log)
      },

    BuscarPaciente(doc) {
      console.log(doc);
      fetch('http://localhost/API/?consultar='+doc) //se hace uso de la API para consultar un paciente por numero de documento
      .then(response=>response.json())
      .then((data) => {
        if(typeof data[0].sucess==='undefined'){
          this.pacienteEncontrado=data
          console.log(data);
        }
        
        else {
          console.log('Paciente no encontrado');
          this.mensajeError = 'Paciente no encontrado';
          this.pacienteEncontrado = null; // Reinicia los datos si no se encuentra el paciente
        }
        })

        .catch((error) => {
        // Manejo de errores
        console.log('Error al buscar el paciente:', error);
        this.mensajeError = 'Error al buscar el paciente.';
      });
  }
},

}
</script>
  