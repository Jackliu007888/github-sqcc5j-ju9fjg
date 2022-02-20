<template>
  <client-only>
    <a-cascader
      v-model:value="value"
      :options="options"
      :load-data="loadData"
      placeholder="Please select"
      change-on-select
    />
  </client-only>
</template>
<script setup>

const value = useState('value', () => [])

const options = useState('options', () => [{
  value: 'zhejiang',
  label: 'Zhejiang',
  isLeaf: false,
}, {
  value: 'jiangsu',
  label: 'Jiangsu',
  isLeaf: false,
}])

const loadData = selectedOptions => {
  const targetOption = selectedOptions[selectedOptions.length - 1]
  targetOption.loading = true // load options lazily

  setTimeout(() => {
    targetOption.loading = false
    targetOption.children = [{
      label: `${targetOption.label} Dynamic 1`,
      value: 'dynamic1',
    }, {
      label: `${targetOption.label} Dynamic 2`,
      value: 'dynamic2',
    }]
    options.value = [...options.value]
  }, 1000)
}
</script>
