<template>
  <div class="space-x-launches">
    <h1>SpaceX Launches</h1>
    <ul>
      <li v-for="launch in launches" :key="launch.mission_name">
        <h2>{{ launch.mission_name }}</h2>
        <p>Launch Date: {{ launch.launch_date_local }}</p>
        <p>Launch Site: {{ launch.launch_site.site_name_long }}</p>
        <p>Rocket: {{ launch.rocket.rocket_name }}</p>
        <p>Article Link: <a :href="launch.links.article_link" target="_blank">{{ launch.links.article_link }}</a></p>
        <p>Video Link: <a :href="launch.links.video_link" target="_blank">{{ launch.links.video_link }}</a></p>
      </li>
    </ul>
  </div>
</template>

<script>
import { ApolloClient, gql, InMemoryCache } from '@apollo/client';

const apolloClient = new ApolloClient({
  uri: 'https://spacex-production.up.railway.app/',
  cache: new InMemoryCache(),
});

export default {
  name: 'SpaceXLaunches',
  data() {
    return {
      launches: [],
    };
  },
  async created() {
    const { data } = await apolloClient.query({
      query: gql`
        query GetLaunches {
          launchesPast(limit: 10) {
            mission_name
            launch_date_local
            launch_site {
              site_name_long
            }
            links {
              article_link
              video_link
            }
            rocket {
              rocket_name
            }
          }
        }
      `,
    });

    this.launches = data.launchesPast;
  },
};
</script>

<style scoped>
/* Add your styles here */
</style>
