<template>
  <v-app id="inspire" >
    <v-navigation-drawer
      :clipped="drawer.clipped"
      :fixed="drawer.fixed"
      :mini-variant="drawer.mini"
      v-model="drawer.open"
      app>
      <v-list dense>
        <v-list-tile nuxt :to="menu.home">
          <v-list-tile-action>
            <v-icon>home</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Home</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile nuxt :to="menu.reservation">
          <v-list-tile-action>
            <v-icon>assignment</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Reservation</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile nuxt :to="menu.setting">
          <v-list-tile-action>
            <v-icon>settings</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Settings</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar fixed app clipped-left>
      <v-toolbar-side-icon @click.stop="toggleDrawer"></v-toolbar-side-icon>
      <v-toolbar-title>BANA-NA</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>search</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>refresh</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>account_circle</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>more_vert</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <nuxt/>
    </v-content>
    <v-footer dark app>
      <span class="white--text">&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: {
      open: true,
      clipped: true,
      fixed: true,
      mini: false
    },
    menu: {
      home: '/',
      reservation: '/reservation',
      setting: '/setting'
    },
    accounts: [
      ['Group', 'people_outline'],
      ['Settings', 'settings']
    ]
  }),
  props: {
    source: String
  },
  methods: {
    toggleDrawer() {
      this.drawer.open = !this.drawer.open;
    }
  }
}
</script>
