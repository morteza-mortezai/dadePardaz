<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      color="background"
      :mini-variant="mini_variant"
      fixed
      app
      right
    >
      <!-- main navigation -->
      <navigation />
    </v-navigation-drawer>
    <v-app-bar fixed app elevate-on-scroll color="background" dense>
      <!-- toggle -->
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer></v-spacer>
      <!-- notif dropdown -->
      <v-menu bottom left offset-y>
        <template #activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" small v-on="on">
            <v-avatar>
              <v-icon>mdi-bell</v-icon>
            </v-avatar>
          </v-btn>
        </template>

        <v-list nav dense>
          <v-list-item v-for="(item, i) in notifs" :key="i" two-line>
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
              <v-list-item-subtitle>
                {{ item.sub }}
              </v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-menu>
      <!-- account dropdown -->
      <v-menu bottom left offset-y>
        <template #activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-avatar>
              <v-icon>mdi-account-circle</v-icon>
            </v-avatar>
          </v-btn>
        </template>

        <v-list width="200px" nav dense>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title> نام کاربر</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-power</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title> خروج</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <v-main>
      <v-container class="bg-red">
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Navigation from '~/components/Layouts/Default/Navigation/Navigation.vue'
@Component({ components: { Navigation } })
export default class Layout extends Vue {
  drawer: Boolean = false
  fixed: Boolean = false

  notifs: any = [
    {
      title: 'عنوان',
      sub: 'توضیحات مختصر ',
    },
    {
      title: 'عنوان',
      sub: 'توضیحات مختصر ',
    },
    {
      title: 'عنوان',
      sub: 'توضیحات مختصر ',
    },
  ]


  mini_variant: Boolean = false
}
</script>
<style lang="scss">
.home-enter-active,
.home-leave-active {
  transition: opacity 0.5s;
}
.home-enter,
.home-leave-active {
  opacity: 0;
}
#app {
  background-color: var(--v-background-base) !important;
}
</style>
