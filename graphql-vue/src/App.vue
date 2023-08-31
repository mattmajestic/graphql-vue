<template>
  <div id="app">
    <SpaceXLaunches />
  </div>
</template>

<script>
import Vue from 'vue';
import SpaceXLaunches from './components/SpaceXLaunches.vue';
import { ApolloClient, InMemoryCache } from '@apollo/client';

const apolloClient = new ApolloClient({
  uri: 'https://spacex-production.up.railway.app/',
  cache: new InMemoryCache(),
});

Vue.use({
  install(Vue) {
    Vue.prototype.$apollo = apolloClient;
  },
});

export default {
  name: 'App',
  components: {
    SpaceXLaunches,
  },
};
</script>
