<template>
    <div id="app">
        持续集成
    </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue'
import { useStore } from 'vuex'
import axios from '@/apis'

interface ResData {
  user: {
    name: String
    child: {
      name: string
    }[]
  }[]
}

export default defineComponent({
    setup() {
        const store = useStore()
        const data = reactive({
            show: true,
        })
        console.log(
            `VUEP_BASE_URL=${process.env.VUE_BASE_URL}`,
            process.env.BUILD_TIME
        )
        setInterval(() => {
        store.dispatch('countUp')
        }, 1000)
        axios.get<ResData>('../static/head.json', {}).then((res) => {
        console.log(res)
        })
        return { ...toRefs(data) }
    },
})
</script>
