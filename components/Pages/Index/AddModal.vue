<template>
  <v-dialog v-model="show" width="500">
    <v-card>
      <v-card-title class="text-h5 grey lighten-2"> افزودن </v-card-title>

      <v-card-text class="py-5">
        <v-row>
          <!-- name -->
          <v-col cols="6">
            <v-text-field
              v-model="form.name"
              dense
              hide-details
              label="نام"
            ></v-text-field>
          </v-col>
          <!-- count -->
          <v-col cols="6">
            <v-text-field
              v-model="form.count"
              type="number"
              dense
              hide-details
              label="تعداد"
            ></v-text-field>
          </v-col>
          <!-- date -->
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
                  :value="convertDate(form.date)"
                  label="تاریخ"
                  prepend-icon="mdi-calendar"
                  readonly
                  v-bind="attrs"
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker
                v-model="form.date"
                locale="fa-IR"
                @input="dateMenu = false"
              ></v-date-picker>
            </v-menu>
          </v-col>
        </v-row>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="error" @click="show = false" small> انصراف </v-btn>
        <v-btn color="success" @click="save" small> ذخیره </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { Component, Vue, VModel, Emit } from 'vue-property-decorator'

@Component({ components: {} })
export default class AddModal extends Vue {
  @VModel({ default: false }) show!: boolean
  form = {}
  dateMenu = false
  save() {
    this.onAdd()
    this.show = false
  }

  convertDate(d: string) {
    if (!d) return null
    const date = new Date(d)
    return date.toLocaleDateString('fa-IR')
  }

  @Emit()
  onAdd() {
    return this.form
  }
}
</script>
