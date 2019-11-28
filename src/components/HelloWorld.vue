<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex xs12>
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        ></v-img>
      </v-flex>

      <v-flex md12 mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          Bem Vindo ao Atacado
        </h1>
        <p class="subheading font-weight-regular">
          Aplicação criada apenas para demonstração na disciplina de Sistemas Distribuídos,
          <br>Direitos reservados a Manoel Tavares
        </p>
      </v-flex>

      <v-flex md12 mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          Estatisticas
        </h1>
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Nome</th>
                <th class="text-left">Email</th>
                <th class="text-right">Pontos</th>
                <th class="text-right">Compras</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item,idx) in users" :key="idx">
                <td class="text-left">{{ item.name }}</td>
                <td class="text-left">{{ item.email }}</td>
                <td class="text-right">{{ item.pontos || 0}}</td>
                <td class="text-right">{{ item.compras || 0}}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-flex>

      
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',

  data: () => ({
    userCount: 0,
    users: [],
  }),
  methods: ({
    getStats(){
      axios.get('http://localhost:3000/stats')
        .then(res => {
          this.userCount = res.data.users,
          this.users = res.data.lastInto
        })
    }
  }),
  mounted(){
    this.getStats();
  }
};
</script>
