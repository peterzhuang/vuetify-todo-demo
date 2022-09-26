<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer"
      :mobile-breakpoint="768"
      app
    >
    <v-img
      class="pa-4 pt-7"
      src="mountain.jpg"
      height="170"
      gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
    >
    <v-avatar size="70" class="mb-2">
      <img
        src="https://avatars.githubusercontent.com/u/7306753?v=4"
        alt="Yuchuan"
      >
    </v-avatar>
    <div class="white--text text-subtitle-1 font-weight-bold">Yuchuan Zhuang</div>
    </v-img>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>


    <v-app-bar
      app
      color="primary"
      dark
      src="mountain.jpg"
      prominent
      height="170"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-app-bar-title class="ml-4 text-h4">
            {{ $store.state.appTitle }}
          </v-app-bar-title>
        </v-row>
        <v-row>
          <live-date-time />
        </v-row>
      </v-container>

    </v-app-bar>


    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
  import Snackbar from '@/components/Shared/Snackbar.vue';
  import Search from '@/components/Tools/Search.vue';
  import LiveDateTime from './components/Tools/LiveDateTime.vue';

  export default {
    data: () => ({ 
      drawer: null,
      items: [
          { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
          { title: 'About', icon: 'mdi-help-box', to: '/about' },
        ],
    }),
    // computed: {
    //   appTitle() {
    //     return process.env.VUE_APP_TITLE;
    //   }
    // },
    mounted() {
      this.$store.dispatch('getTasks');
    },
    components: {
      'search': Search,
      'live-date-time': LiveDateTime,
      'snackbar': Snackbar
    }
  }
</script>

<style lang="sass">
  .header-container
    max-width: none !important
</style>