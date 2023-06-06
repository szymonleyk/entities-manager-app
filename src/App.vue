<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item :prepend-avatar="require('./assets/profile.png')" title="Szymon Leyk" nav></v-list-item>
      </v-list>

      <v-list-item v-for="item in items" :key="item.title" :prepend-icon="item.icon" :title="item.title"
        :value="item.value" :to="item.to" link>
      </v-list-item>
    </v-navigation-drawer>

    <v-app-bar>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Entities Manager</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Dashboard', value: 'dashboard', icon: 'mdi-view-dashboard', to: '/' },
      { title: 'Profile', value: 'profile', icon: 'mdi-account', to: '/profile' },
      { title: 'Logout', value: 'logout', icon: 'mdi-logout-variant', to: '/logout' }
    ]
  }),
}
</script>