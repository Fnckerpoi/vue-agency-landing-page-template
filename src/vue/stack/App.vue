<template>
    <!-- 处理全局状态 -->
    <StateProviderLayer>
        <!-- 处理 UI 反馈，例如加载程序和活动旋转器 -->
        <FeedbacksLayer>
            <!-- 处理路线/模式 -->
            <ContentLayer>
                <!-- 应用内容 -->
                <Master/>
            </ContentLayer>
        </FeedbacksLayer>
    </StateProviderLayer>
</template>

<script setup>
import StateProviderLayer from "/src/vue/stack/StateProviderLayer.vue"
import FeedbacksLayer from "/src/vue/stack/FeedbacksLayer.vue"
import ContentLayer from "/src/vue/stack/ContentLayer.vue"
import Master from "/src/vue/content/Master.vue"
import {useEmails} from "/src/composables/emails.js"
import {onMounted} from "vue"

const emails = useEmails()

onMounted(() => {
    emails.init()
})
</script>

<style lang="scss" scoped>
</style>