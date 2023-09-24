<template>
  <q-page>
    <div class="q-mt-md q-ml-md row">
      <q-input style="width:200px" outlined v-model="tableName" label="Table Name"></q-input>
      <q-btn class="q-ml-md" label="Filter" dense push color="positive" no-caps @click="filterFollowTableName"></q-btn>
    </div>

    <div class="q-mt-md q-ml-md row">
      <q-input style="width:200px" outlined v-model="columnName" label="Column Name"></q-input>
      <q-btn class="q-ml-md" label="Filter" dense push color="positive" no-caps @click="filterFollowColumnName"></q-btn>
    </div>

    <div class="flex flex-center">
      <div>We have found {{ this.infoTables.length }} tables  </div>

    </div>
    <div class="row">
      <div v-for="table in this.infoTables ">
        <TableInfoBox :table="table"></TableInfoBox>
      </div>

    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import axios from 'axios'
import { WebApi } from "/src/api/WebApi";
import TableInfoBox from "/src/components/TableInfoBox.vue"
export default defineComponent({
  name: 'IndexPage',
  components: { TableInfoBox },
  setup() {
    console.log("hi")
    // axios.get(`${WebApi.server}/infoColumn`).then(res => {
    //   console.log("Column Info ", res.data)
    // })
    const infoColumns = ref([])
    const infoTables = ref([])
    return {
      infoColumns,
      tableName: ref(''),
      columnName: ref(''),
      infoTables
    }
  },
  methods: {
    filterFollowTableName() {
      axios.get(`${WebApi.server}/infoColumn/tableName/` + this.tableName).then(res => {
        this.infoColumns = res.data
        console.log("Column Info ", this.infoColumns)
      })
    },
    filterFollowColumnName(){
      axios.get(`${WebApi.server}/infoColumn/table/` + this.tableName+'/column/'+this.columnName).then(res => {
        this.infoTables = res.data
        console.log("Column Info ", this.infoTables)
      })
    }
  }
})

</script>
