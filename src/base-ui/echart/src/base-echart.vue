<template>
  <div class="base-echart">
    <div
      ref="echartDivRef"
      :style="{ width: props.width, height: props.height }"
    ></div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref, watchEffect } from 'vue'
import * as echarts from 'echarts'
import useEcharts from '../hooks/useEchart'
type EChartsOption = echarts.EChartsOption
const props = withDefaults(
  defineProps<{
    options: EChartsOption
    width?: string
    height?: string
  }>(),
  {
    width: '100%',
    height: '360px'
  }
)

const echartDivRef = ref<HTMLElement>()

onMounted(() => {
  const { setOptions } = useEcharts(echartDivRef.value!)
  watchEffect(() => {
    setOptions(props.options)
  })
})
</script>

<style scoped lang="less"></style>
