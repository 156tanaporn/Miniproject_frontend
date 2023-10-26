<template>
  <div>
  <v-data-table
      :headers="headers"
      :items="seriesItem"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar
          flat
        >
          <v-toolbar-title>จัดการข้อมูล</v-toolbar-title>
          <v-divider
            class="mx-4"
            inset
            vertical
          ></v-divider>
          <v-spacer></v-spacer>
          <v-btn
                color="primary"
                dark
                class="mb-2"
                @click="openDialog('add', defaultItem)"
              >
                เพิ่มข้อมูล
              </v-btn>

        </v-toolbar>
      </template>
      <template v-slot:[`item.actions`] = "{ item }">
        <v-btn small outlined @click="openDialog('edit', item)" color="blue">
        <v-icon>
          mdi-pencil
        </v-icon>
        </v-btn>
        <v-btn small outlined @click="deleteItem(item)" color="red" class="ml-2">
        <v-icon>
          mdi-delete
        </v-icon>
        </v-btn>
      </template>
      <template v-slot:no-data>
        <v-btn
          color="primary"
          @click="initialize"
        >
          Reset
        </v-btn>
      </template>
    </v-data-table>
    <v-dialog
      v-model="dialogCreate"
      max-width="500px"
    >
            <v-card>
              <v-card-title>
                <span class="text-h5">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col
                      cols="12"
                      sm="6"
                      md="6"
                    >
                      <v-text-field
                        v-model="seriesName"
                        label="ชื่อ"
                      ></v-text-field>
                    </v-col>
                    <v-col
                      cols="12"
                      sm="6"
                      md="6"
                    >
                      <v-text-field
                        v-model="detailSeries"
                        label="รายละเอียด"
                      ></v-text-field>
                    </v-col>

                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                  color="blue darken-1"
                  text
                  @click="close"
                >
                  ยกเลิก
                </v-btn>
                <v-btn
                  color="blue darken-1"
                  text
                  @click="save(formTitle)"
                >
                  บันทึกข้อมูล
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="text-h5">ตุณต้องการลบข้อมูลนี้ในตารางใช่ หรือ ไม่?</v-card-title>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete">ยกเลิก</v-btn>
                <v-btn color="blue darken-1" text @click="deleteItemConfirm">ตกลง</v-btn>
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
  </div>
  </template>

<script>
export default {
  data: () => ({
    seriesName: '',
    detailSeries: '',
    dialogCreate: false,

    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: 'id',
        align: 'start',
        sortable: false,
        value: 'seriesId'
      },
      { text: 'ชื่อ', value: 'seriesName' },
      { text: 'รายละเอียด', value: 'detailSeries' },
      { text: 'จัดการ', value: 'actions', sortable: false }
    ],
    seriesItem: [],
    editedIndex: -1,
    editedItem: {
      seriesName: '',
      detailSeries: ''
    },
    defaultItem: {
      seriesName: '',
      detailSeries: ''
    },
    formTitle: '',
    seriesId: '',
    idforDelete: ''
  }),

  watch: {
    dialog (val) {
      val || this.close()
    },
    dialogDelete (val) {
      val || this.closeDelete()
    }
  },

  created () {
    this.initialize()
  },

  methods: {
    async initialize () {
      this.seriesItem = []
      try {
        var data = await this.axios.get('http://localhost:9000/series')
        console.log('data series ===>', data)
        this.seriesItem = data.data
      } catch (error) {

      }
    },

    openDialog (Action, item) {
      this.formTitle = ''
      if (Action === 'add') {
        this.dialogCreate = true
        this.formTitle = 'เพิ่มข้อมูล'
      } else {
        this.formTitle = 'แก้ไขข้อมูล'
        this.dialogCreate = true
        this.seriesName = item.seriesName
        this.detailSeries = item.detailSeries
        this.seriesId = item.seriesId
      }
    },

    editItem (item) {
      console.log('item select', item)
      console.log('index item', this.seriesItem.indexOf(item))
      this.editedIndex = this.seriesItem.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },

    deleteItem (item) {
      this.idforDelete = item.seriesId
      this.dialogDelete = true
    },

    async deleteItemConfirm () {
      try {
        var response = await this.axios.delete('http://localhost:9000/series/' + this.idforDelete)
        this.initialize()
      } catch (error) {
        console.log(error.message)
      }
      this.closeDelete()
    },

    close () {
      this.dialogCreate = false
      this.editedItem = []
      this.editedIndex = -1
      this.defaultItem = {
        seriesName: '',
        detailSeries: ''
      }
    }
  },

  closeDelete () {
    this.dialogDelete = false
    this.$nextTick(() => {
      this.editedItem = Object.assign({}, this.defaultItem)
      this.editedIndex = -1
    })
  },

  async save (action) {
    var data = {
      seriesName: this.seriesName,
      detailSeries: this.detailSeries,
    }
    if (action === 'เพิ่มข้อมูล') {
      console.log('data after send ===>', data)
      try {
        var dataResponse = await this.axios.post('http://localhost:9000/series', data)

        console.log('dataResponse ===>', dataResponse)
        this.close()
        this.initialize()
      } catch (error) {
        console.log(error.message)
      }
    } else {
      try {
        var dataResponseEdit = await this.axios.put('http://localhost:9000/series/' + this.seriesId, data)
        console.log('dataResponse ====>', dataResponseEdit)
        this.close()
        this.initialize()
      } catch (error) {
        console.log(error.message)
      }
    }
  }
}

</script>

<style>

</style>
