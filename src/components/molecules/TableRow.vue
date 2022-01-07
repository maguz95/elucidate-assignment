<template>
  <div
    class="grid grid-cols-[repeat(6,_minmax(250px,_1fr))] gap-3 text-left py-3 border-b hover:bg-slate-200 px-10">
    <div>
      {{ content.body.bankName}}
    </div>
    <div>
      {{ content.body.bankBIC[0] }}
    </div>
    <div>
      {{ reportScore }}
    </div>
    <div>
      {{ content.body.type}}
    </div>
    <div>
      {{ createdAt }}
    </div>
    <div>
      {{ publishedAt }}
    </div>
  </div>
</template>

<script>
import { computed } from "vue"
import dayjs from "dayjs"

export default {
  props: {
    content: {
      type: Object,
      required: true,
    },
  },
  setup (props) {

  const reportScore = computed(() => {
      return Math.round(parseFloat(props.content.body.reportScore) * 1000) / 1000
    })

    const createdAt = computed(() => {
      return dayjs(props.content.createdAt).format("MM/DD/YYYY HH:mm")
    })

    const publishedAt = computed(() => {
      return dayjs(props.content.publishedAt).format("MM/DD/YYYY HH:mm")
    })

    return {
      reportScore,
      createdAt,
      publishedAt
    }
  }
}
</script>

<style lang="scss" scoped>

</style>