<template>
  <section>
    <v-text-field
      v-model="search"
      dense
      append-icon="mdi-magnify"
      flat
      filled
      autofocus
    />
    <v-list nav dense>
      <v-list-group
        v-for="item in filteredMenu"
        :key="item.title"
        v-model="item.active"
        class="border-left"
        no-action
      >
        <template #activator>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"></v-list-item-title>
          </v-list-item-content>
        </template>
        <template #prependIcon>
          <v-tooltip right>
            <template #activator="{ on, attrs }">
              <v-icon v-bind="attrs" v-on="on"> {{ item.action }} </v-icon>
            </template>
            <span>{{ item.title }}*</span>
          </v-tooltip>
        </template>
        <v-list-item
          v-for="child in item.items"
          :key="child.title"
          :to="child.to"
          active-class="primary--text"
          dense
          style="min-height: 30px; padding-left: 33px"
        >
          <v-list-item-title
            class="pa-0"
            v-text="child.title"
          ></v-list-item-title>
        </v-list-item>
      </v-list-group>
    </v-list>
  </section>
</template>
<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator'

@Component
export default class NavigationComponent extends Vue {
  search: string = ''
  menu = [
    {
      action: 'mdi-home',
      active: false,
      items: [{ title: 'داشبورد', to: '/' }],
      title: 'خانه',
    },
    {
      action: 'mdi-cube-outline',
      active: false,
      items: [{ title: 'لیست محصولات', to: '/products' }],
      title: 'محصولات',
    },
    {
      action: 'mdi-account-multiple-outline',
      active: false,
      items: [{ title: 'لیست کاربران', to: '/users' }],
      title: 'کاربران',
    },
    {
      action: 'mdi-account-box',
      active: false,
      items: [{ title: 'لیست نمایندگی ها', to: '/resellers' }],
      title: 'نمایندگی ها',
    },
    {
      action: 'mdi-home',
      active: false,
      items: [{ title: 'داشبورد', to: '/service1' }],
      title: 'خدمات',
    },
    {
      action: 'mdi-information-variant',
      active: false,
      items: [{ title: 'درباره ما', to: '/about' }],
      title: 'درباره ما',
    },
    {
      action: 'mdi-phone',
      active: false,
      items: [{ title: 'آدرس', to: '/address' }],
      title: 'تماس با ما',
    },
    {
      action: 'mdi-account-box',
      active: false,
      items: [{ title: 'شماره های تماس', to: '/' }],
      title: 'ارتباط',
    },
  ]

  get filteredMenu() {
    if (this.search) {
      return this.menu.filter((item) => {
        return item.title.includes(
          this.search?.trim().toLocaleLowerCase('fa-IR')
        )
      })
    } else {
      return this.menu
    }
  }
}
</script>
