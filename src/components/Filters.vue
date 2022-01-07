<template>
  <div class="px-10">
    <p class="text-xl font-bold text-left">Filter your data</p>
    <div class="grid grid-cols-1 gap-20 px-5 py-5 mb-5 border md:grid-cols-2 lg:grid-cols-5">
      <label class="flex flex-col text-left">
        Bank name
        <input type="text" placeholder="Bank name" v-model="filterForm.bankName" class="px-2 py-3 rounded-md accent-slate-500 bg-slate-300">
      </label>
      <label class="flex flex-col text-left">
        Bank BIC
        <input type="text" placeholder="Bank BIC" v-model="filterForm.bankBIC" class="px-2 py-3 rounded-md accent-slate-500 bg-slate-300">
      </label>
      <label class="flex flex-col text-left">
        Type of report
        <select v-model="filterForm.reportType" class="px-2 py-3 rounded-md accent-slate-500 bg-slate-300">
          <option value="">All</option>
          <option value="extended">Extended</option>
          <option value="intermediate">Intermediate</option>
          <option value="primary">Primary</option>
        </select>
      </label>
      <label class="flex flex-col text-left">
        Score range
        <div class="h-[46px] flex items-center">
          <Slider v-model="filterForm.range" class="w-40" show-tooltip="drag" :max="200" />
        </div>
      </label>
      <label class="flex flex-col text-left">
        Publish status
        <select v-model="filterForm.published" class="px-2 py-3 rounded-md accent-slate-500 bg-slate-300">
        <option value="">All</option>
        <option value="published">Published</option>
        <option value="not_published">Not published</option>
        </select>
      </label>
    </div>
  </div>
</template>

<script>
import {reactive, watch} from 'vue'

import Slider from '@vueform/slider'

export default {
  name: 'ElucidateFilters',
  components: {
    Slider,
  },
  setup (_, context) {
    const filterForm = reactive({
      bankName: '',
      bankBIC: '',
      reportType: '',
      range: [0, 200],
      published: '',
    })

    watch(filterForm, () => {
      context.emit('filter', filterForm)
    })

    return {
      filterForm
    }
  }
}
</script>

<style src="@vueform/slider/themes/default.css"></style>