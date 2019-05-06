<template>
  <div>
    <h1>Lista de deputados</h1>
    <ul class="list">
      <li class="item" v-for="deputados in getDeputados" :key="deputados.node.id">
        <img class="avatar" :src="deputados.node.urlFoto" :alt="deputados.node.nome">
        <div>
          {{ deputados.node.nome }} / {{ deputados.node.siglaPartido }}
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'home',
  // Configure in .env VUE_APP_GRAPHQL_URL=https://graphql-camara-deputados.herokuapp.com/
  // to example works
  apollo: {
    deputados: gql`query {
      deputados (first: 20) {
        edges {
          node {
            id
            nome
            siglaPartido
            urlFoto
          }
        }
      }
    }`
  },
  computed: {
    getDeputados () {
      if (this.deputados) {
        return this.deputados.edges
      }
      return []
    }
  }
}
</script>

<style scoped>
.list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}
.item {
  text-align: center;
}
.avatar {
  width: 100px;
}
</style>
