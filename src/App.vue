<template>
    <div id="app">
        脚手架 + vue3-ts模版 + travis 实现项目搭建，持续集成 + 部署
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
