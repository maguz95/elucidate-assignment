<template>
  <e-filters @filter="filterData($event)"></e-filters>
  <e-table :content="currentPageData" @sort="sortData"></e-table>
  <e-pagination
    v-if="itemsAmount > 0"
    :items-amount="itemsAmount"
    :items-per-page="10"
    @change-page="getPageData"></e-pagination>
  <div v-else>
    No data found
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import ElucidateTable from './components/Table.vue'
import ElucidateFilters from './components/Filters.vue'
import ElucidatePagination from './components/molecules/Pagination.vue'
import dayjs from 'dayjs'

export default {
  name: 'App',
  components: {
    'e-table': ElucidateTable,
    'e-filters': ElucidateFilters,
    'e-pagination': ElucidatePagination,
  },
  setup () {
    const data = ref([])
    const displayData = ref([])
    const currentPageData = ref([])
    const itemsAmount = ref(0)
    const pageSize = ref(10)

    onMounted(async () => {
      data.value = await fetch('resources/reports.json')
        .then(response => response.json())
      displayData.value = data.value
      itemsAmount.value = data.value.length
      getPageData(1)
    });

    const getPageData = (page) => {
      currentPageData.value = displayData.value.slice(
        (page - 1) * pageSize.value,
        page * pageSize.value
      )
    }

    const filterData = (filterForm) => {
      displayData.value = data.value
      if(filterForm.bankName) {
        displayData.value = displayData.value.filter(item => item.body.bankName.toLowerCase().includes(filterForm.bankName.toLowerCase()))
      }

      if(filterForm.bankBIC) {
        displayData.value = displayData.value.filter(item => item.body.bankBIC.toLowerCase().includes(filterForm.bankBIC.toLowerCase()))
      }

      if(filterForm.reportType) {
        displayData.value = displayData.value.filter(item => item.body.type.toLowerCase().includes(filterForm.reportType.toLowerCase()))
      }

      if(filterForm.range) {
        displayData.value = displayData.value.filter(item => item.body.reportScore >= filterForm.range[0] && item.body.reportScore <= filterForm.range[1])
      }

      if(filterForm.published === 'published'){
        displayData.value = displayData.value.filter(item => dayjs(item.publishedAt).isBefore(dayjs()))
      } else if(filterForm.published === 'not_published'){
        displayData.value = displayData.value.filter(item => dayjs(item.publishedAt).isAfter(dayjs()))
      }

      getPageData(1)
      itemsAmount.value = displayData.value.length
    }

    const sortData = (sort) => {
      displayData.value = data.value
      displayData.value = displayData.value.sort((a, b) => {
        if(sort.direction === 'asc'){
          if(sort.field !== 'createdAt' && sort.field !== 'publishedAt'){
            return a.body[sort.field] > b.body[sort.field] ? 1 : -1
          } else {
            return dayjs(a[sort.field]).isAfter(dayjs(b[sort.field])) ? 1 : -1
          }
        } else if(sort.direction === 'desc') {
          if(sort.field !== 'createdAt' && sort.field !== 'publishedAt'){
            return a.body[sort.field] < b.body[sort.field] ? 1 : -1
          } else {
            return dayjs(a[sort.field]).isBefore(dayjs(b[sort.field])) ? 1 : -1
          }
        }
      })
      getPageData(1)
    }

    return {
      getPageData,
      currentPageData,
      itemsAmount,
      filterData,
      sortData
    }
  }
}
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
