/* eslint-disable vue/valid-v-slot */
<template>
  <v-row justify="center" align="center">
    <!-- add modal -->
    <add-modal v-model="addModal" @on-add="onAdd" />
    <!-- header -->
    <v-col cols="12">
      <v-list-item>
        <v-list-item-icon>
          <v-icon v-text="'mdi-cube-outline'"></v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title v-text="'لیست کالاهای موجود'"></v-list-item-title>
        </v-list-item-content>
        <v-list-item-action>
          <v-btn icon color="success" @click="addModal = true">
            <v-icon> mdi-plus </v-icon>
          </v-btn>
        </v-list-item-action>
      </v-list-item>
    </v-col>
    <!-- filter name -->
    <v-col cols="6">
      <v-text-field v-model="name" label="نام" clearable></v-text-field>
    </v-col>
    <!-- filter date -->
    <v-col cols="6">
      <v-menu
        v-model="dateMenu"
        :close-on-content-click="false"
        :nudge-right="40"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template #activator="{ on, attrs }">
          <v-text-field
            :value="convertDate(date)"
            label="تاریخ"
            prepend-icon="mdi-calendar"
            v-bind="attrs"
            clearable
            @input="date = $event"
            v-on="on"
          >
          </v-text-field>
        </template>
        <v-date-picker
          v-model="date"
          locale="fa-IR"
          @input="dateMenu = false"
        ></v-date-picker>
      </v-menu>
    </v-col>
    <!-- table -->
    <v-col cols="12">
      <v-data-table
        :items="filteredItems"
        :headers="headers"
        dense
        locale="fa-IR"
      >
        <template #item.date="{ item }">
          {{ convertDate(item.date) }}
        </template>
        <template #item.count="{ item }">
          {{ item.count.toLocaleString('fa-IR') }}
        </template>
      </v-data-table>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import AddModal from '~/components/Pages/Index/AddModal.vue'
@Component({ components: { AddModal } })
export default class Index extends Vue {
  addModal = false
  dateMenu = false
  date = null
  name: any = null
  items = [
    {
      name: 'کالای اول',
      count: 10,
      date: '2021-12-12',
      a: 'a',
      b: 'b',
      c: 'c',
      d: 'd',
      e: 'e',
      f: 'f',
      g: 'g',
      h: 'h',
      i: 'i',
      j: 'j',
      k: 'k',
      l: 'l',
      m: 'm',
      n: 'n',
      o: 'o',
      p: 'p',
      q: 'q',
      r: 'r',
      s: 's',
    },
    {
      name: 'کالای دوم',
      count: 10,
      date: '2022-02-12',
      a: 'a',
      b: 'b',
      c: 'c',
      d: 'd',
      e: 'e',
      f: 'f',
      g: 'g',
      h: 'h',
      i: 'i',
      j: 'j',
      k: 'k',
      l: 'l',
      m: 'm',
      n: 'n',
      o: 'o',
      p: 'p',
      q: 'q',
      r: 'r',
      s: 's',
    },
    {
      name: 'کالای سوم',
      count: 10,
      date: '2022-02-14',
      a: 'a',
      b: 'b',
      c: 'c',
      d: 'd',
      e: 'e',
      f: 'f',
      g: 'g',
      h: 'h',
      i: 'i',
      j: 'j',
      k: 'k',
      l: 'l',
      m: 'm',
      n: 'n',
      o: 'o',
      p: 'p',
      q: 'q',
      r: 'r',
      s: 's',
    },
  ]

  get headers() {
    const a = [
      {
        text: 'نام',
        value: 'name',
        sortable: true,
      },
      {
        text: 'تعداد',
        value: 'count',
        sortable: true,
      },
      {
        text: 'تاریخ',
        value: 'date',
        sortable: true,
      },
    ]
    const arr = [
      'a',
      'b',
      'c',
      'd',
      'e',
      'f',
      'g',
      'h',
      'i',
      'j',
      'k',
      'l',
      'm',
      'o',
      'p',
      'r',
      's',
    ]
    arr.forEach((item) =>
      a.push({
        text: item,
        value: item,
        sortable: false,
      })
    )
    return a
  }

  onAdd(v: any) {
    const item = {
      ...v,
      a: 'a',
      b: 'b',
      c: 'c',
      d: 'd',
      e: 'e',
      f: 'f',
      g: 'g',
      h: 'h',
      i: 'i',
      j: 'j',
      k: 'k',
      l: 'l',
      m: 'm',
      n: 'n',
      o: 'o',
      p: 'p',
      q: 'q',
      r: 'r',
      s: 's',
    }
    this.items.push(item)
  }

  convertDate(d: string) {
    if (!d) return null
    const date = new Date(d)
    return date.toLocaleDateString('fa-IR')
  }

  get filteredItems() {
    return this.items.filter((item) => {
      if (this.date && this.name) {
        return item.date === this.date && item.name.includes(this.name.trim())
      } else if (this.name) {
        return item.name.includes(this.name.trim())
      } else if (this.date) {
        return item.date === this.date
      }
      return item
    })
  }
}
</script>
