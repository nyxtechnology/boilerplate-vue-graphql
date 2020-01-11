<template>
  <div>
    <h1>
      <svg-icon name="bundle" title="budle" />
      <span>{{ $t('title_home') }}</span>
    </h1>

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
import SvgIcon from '@components/SvgIcon'

export default {
  name: 'home',
  components: {
    SvgIcon
  },
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
