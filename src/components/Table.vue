<template>
  <div class="overflow-x-hidden">
    <div class="grid grid-flow-row px-10 overflow-scroll">
      <div class="grid grid-cols-[repeat(6,_minmax(250px,_1fr))] gap-3 text-left py-2 font-bold uppercase bg-slate-400 px-10 w-full">
        <div @click="sort('bankName')" class="flex items-center gap-1">
          Bank name
          <span v-if="orderColumn === 'bankName' && orderDirection === 'asc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-down" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 9 12 15 18 9" />
            </svg>
          </span>
          <span v-else-if="orderColumn === 'bankName' && orderDirection === 'desc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-up" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 15 12 9 18 15" />
            </svg>
          </span>
        </div>
        <div @click="sort('bankBIC')" class="flex items-center gap-1">
          Bank BIC
          <span v-if="orderColumn === 'bankBIC' && orderDirection === 'asc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-down" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 9 12 15 18 9" />
            </svg>
          </span>
          <span v-else-if="orderColumn === 'bankBIC' && orderDirection === 'desc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-up" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 15 12 9 18 15" />
            </svg>
          </span>
        </div>
        <div @click="sort('reportScore')" class="flex items-center gap-1">
          Report score value
          <span v-if="orderColumn === 'reportScore' && orderDirection === 'asc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-down" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 9 12 15 18 9" />
            </svg>
          </span>
          <span v-else-if="orderColumn === 'reportScore' && orderDirection === 'desc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-up" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 15 12 9 18 15" />
            </svg>
          </span>
        </div>
        <div @click="sort('type')" class="flex items-center gap-1">
          Type of report
          <span v-if="orderColumn === 'type' && orderDirection === 'asc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-down" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 9 12 15 18 9" />
            </svg>
          </span>
          <span v-else-if="orderColumn === 'type' && orderDirection === 'desc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-up" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 15 12 9 18 15" />
            </svg>
          </span>
        </div>
        <div @click="sort('createdAt')" class="flex items-center gap-1">
          Created at
          <span v-if="orderColumn === 'createdAt' && orderDirection === 'asc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-down" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 9 12 15 18 9" />
            </svg>
          </span>
          <span v-else-if="orderColumn === 'createdAt' && orderDirection === 'desc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-up" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 15 12 9 18 15" />
            </svg>
          </span>
        </div>
        <div @click="sort('publishedAt')" class="flex items-center gap-1">
          Published at
          <span v-if="orderColumn === 'publishedAt' && orderDirection === 'asc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-down" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 9 12 15 18 9" />
            </svg>
          </span>
          <span v-else-if="orderColumn === 'publishedAt' && orderDirection === 'desc'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-chevron-up" width="20" height="20" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <polyline points="6 15 12 9 18 15" />
            </svg>
          </span>
        </div>
      </div>
      <table-row v-for="item in content" :key="item.uuid" :content="item"></table-row>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import TableRow from './molecules/TableRow.vue'
export default {
  components: { TableRow },
  emits: ['sort'],
  name: 'ElucidateTable',
  props: {
    content: {
      type: Object,
      required: true,
    },
  },
  setup (_, context) {
    const orderColumn = ref('')
    const orderDirection = ref('')

    const sort = (field) => {
      if(orderColumn.value !== field){
        orderColumn.value = field
        orderDirection.value = 'asc'
      } else{
        if(orderDirection.value === 'asc'){
          orderDirection.value = 'desc'
        } else {
          orderColumn.value = ''
          orderDirection.value = ''
        }
      }

      console.log(orderColumn.value, orderDirection.value);

      context.emit('sort', {
        field,
        direction: orderDirection.value,
      })
    }

    return {
      orderColumn,
      orderDirection,
      sort
    }
  }
}
</script>

<style lang="scss" scoped>

</style>