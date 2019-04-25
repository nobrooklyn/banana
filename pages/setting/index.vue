<template>
  <v-layout justify-center>
    <v-flex md12>
      <v-card>
        <v-card-title class="headline">Settings</v-card-title>
        <v-tabs icons-and-text grow>
          <v-tabs-slider color="primary"></v-tabs-slider>
          <v-tab nuxt href="#user">
            Users
            <v-icon>person</v-icon>
          </v-tab>
          <v-tab nuxt href="#group">
            Groups
            <v-icon>group</v-icon>
          </v-tab>
          <v-tab nuxt href="#office">
            Offices
            <v-icon>domain</v-icon>
          </v-tab>
          <v-tab nuxt href="#item">
            Items
            <v-icon>category</v-icon>
          </v-tab>

          <v-tab-item id="user">
            <User/>
          </v-tab-item>
          <v-tab-item id="group">
            <Group/>
          </v-tab-item>
          <v-tab-item id="office">
            <Office/>
          </v-tab-item>
          <v-tab-item id="item">
            <Item/>
          </v-tab-item>
        </v-tabs>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import User from "~/pages/setting/user/index.vue";
import Group from "~/pages/setting/group/index.vue";
import Office from "~/pages/setting/office/index.vue";
import Item from "~/pages/setting/item/index.vue";

export default {
  components: {
    User,
    Group,
    Office,
    Item
  }
};
</script>
