<template>
  <q-item clickable @click="displayExtendCard">
    <q-card class="q-ml-sm q-mt-sm" style="min-width:250px; min-height:80px">
      <q-card-section>
        <div class="flex flex-center">{{ table.columns[0].schemaName + '.' + table.tableName }}
          <q-badge>
            {{ table.columns.length }}
          </q-badge>
        </div>
      </q-card-section>
      <q-card-actions v-if="displayCard">
        <div v-for="column in table.columns" :key="column" style="width: 100%;">
          <div class="row q-mb-xs ">
            <div style="
    color: blueviolet;
">
              {{ column.columnName }} :
            </div>
            <div class="q-ml-xs">{{ column.columnType }}</div>
          </div>

        </div>
      </q-card-actions>
    </q-card>
  </q-item>
</template>

<script>
import { ref } from 'vue'
export default {
  props: ['table'],

  setup() {

    return {
      displayCard: ref(false)
    }
  },
  methods: {
    displayExtendCard() {
      if (this.displayCard) {
        this.displayCard = false
      } else {
        this.displayCard = true

      }
    }
  }
}
</script>
