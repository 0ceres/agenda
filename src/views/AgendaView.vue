<template>
    <div>
      <h1>{{ title }}</h1>
      <div class="filtro">
            Filtro: <input type="search" v-model="textoBusar">
      </div>
      <table>
        <thead>
            <tr>
              <th>ID</th>
              <th>Nombre</th>
              <th>Correo electrónico</th>
              <th>Dirección</th>
              <th>Teléfono</th>
              <th>País</th>
              <th>Ciudad</th>
              <th></th>
            </tr>
            <tr>
              <th><input v-if="this.indexEditing !== null" type="text" v-model="contactoObj.id"/></th>
              <th><input type="text" v-model="contactoObj.name"/></th>
              <th><input type="text" v-model="contactoObj.email"/></th>
              <th><input type="text" v-model="contactoObj.address"/></th>
              <th><input type="text" v-model="contactoObj.phone"/></th>
              <th><input type="text" v-model="contactoObj.country"/></th>
              <th><input type="text" v-model="contactoObj.city"/></th>
              <th><button @click="guardar()">Guardar</button></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(contacto, index) in listaContactosComputada" :key="contacto.id">
                <td>{{ contacto.id }}</td>
                <td>{{ contacto.name }}</td>
                <td>{{ contacto.email }}</td>
                <td>{{ contacto.address }}</td>
                <td>{{ contacto.phone }}</td>
                <td>{{ contacto.country }}</td>
                <td>{{ contacto.city }}</td>
                <td>
                    <button @click="editarContacto(contacto, index)">Editar</button>
                    <button @click="eliminarContacto(index)">Eliminar</button>
                </td>
            </tr>
        </tbody>
      </table>
    </div>
  </template>
  
<script>
  export default {
    name: 'MiComponente',
    data() {
      return {
        title: 'Agenda Telefónica',
        textoBusar: '',
        indexEditing: null,
        contactoObj: {
            id: 0,
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        contactos: [
            {
                id: 1,
                name: "Alice Johnson",
                email: "alice.johnson@example.com",
                address: "123 Maple Street",
                phone: "123-456-7890",
                country: "USA",
                city: "New York"
            },
            {
                id: 2,
                name: "Bob Smith",
                email: "bob.smith@example.com",
                address: "456 Oak Avenue",
                phone: "987-654-3210",
                country: "Canada",
                city: "Toronto"
            },
            {
                id: 3,
                name: "Carol White",
                email: "carol.white@example.com",
                address: "789 Pine Road",
                phone: "555-123-4567",
                country: "UK",
                city: "London"
            },
            {
                id: 4,
                name: "David Brown",
                email: "david.brown@example.com",
                address: "321 Elm Street",
                phone: "444-555-6666",
                country: "Australia",
                city: "Sydney"
            },
            {
                id: 5,
                name: "Emily Davis",
                email: "emily.davis@example.com",
                address: "654 Spruce Lane",
                phone: "333-444-5555",
                country: "USA",
                city: "Los Angeles"
            }
        ]
      }
    },
    components: {
      // Registro de componentes que se utilizaran.
    },
    methods: {
      // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
      guardar() {
        if (this.indexEditing === null) {
            var counter = this.contactos.length;
            this.contactoObj.id = counter + 1;
            this.contactos.push(Object.assign({}, this.contactoObj));
        } else {
            this.contactos[this.indexEditing] = Object.assign({}, this.contactoObj);
            this.indexEditing = null;
        }
        this.contactoObj = {
            id: 0,
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        };
      },
      eliminarContacto(index) {
        this.contactos.splice(index, 1);
      },
      editarContacto(contacto, index) {
        this.indexEditing = index;
        this.contactoObj = Object.assign({}, contacto);
      }
    },
    computed: {
      // propiedades computadas que dependen de otras propiedades reactivas
      listaContactosComputada(){
            return this.contactos.filter(item => item.name.toLowerCase().includes(this.textoBusar.toLowerCase())||item.email.toLowerCase().includes(this.textoBusar.toLowerCase()));
        }
    },
    props: {
      // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
  }
  </script>
  
  <style scope>
  h1 {
    color: #42b983;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    padding: 8px;
    border-bottom: 1px solid #ddd;
  }

  th {
    background-color: #f2f2f2;
    text-align: left;
  }
  </style>