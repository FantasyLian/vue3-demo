<template>
  <div class="about">
    <p>第 {{ year }} 年</p>
    <p>姓名：{{ name }}</p>
    <p>年龄：{{ age }}</p>
  </div>
</template>
<script>
import { defineComponent, reactive, ref, toRefs, watch } from 'vue'

export default defineComponent({
  setup () {
    const year = ref(0)
    const state = reactive({ name: 'xiaofeng', age: 20 })

    setInterval(() => {
      year.value++
      state.age++
    }, 1000)

    // watch(
    //   () => state.age,
    //   (curAge, preAge) => {
    //     console.log('新值：', curAge, '旧值：', preAge)
    //   }
    // )
    // watch(year, (newVal, oldVal) => {
    //   console.log('新值：', newVal, '旧值：', oldVal)
    // })

    watch([() => state.age, year], ([curAge, newVal], [preAge, oldVal]) => {
      console.log('新值：', curAge, '旧值：', preAge)
      console.log('新值：', newVal, '旧值：', oldVal)
    })

    return {
      year,
      ...toRefs(state)
    }
  }
})
</script>
