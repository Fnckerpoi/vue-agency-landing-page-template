<template>
    <!-- Heading Section -->
    <PageHeader :id="props.id"
                title="PaoKa"
                subtitle="一天一跑一咖，每天健走十分钟，用脚步连接世界 🏃🌍 跑咖是一个全球运动打卡社区，每天完成运动打卡即可拆开一枚社交盲盒，收获来自全球陌生跑友实拍的风景照片、特殊地点明信片，甚至是一杯真实的咖啡，帮助你养成运动习惯，激励你，陪伴你。"
                logo-url="images/logo/paokalogo_white.png"
                :show-button="true"
                button-icon="fa-solid fa-search"
                button-label="了解我们"
                button-url="#about"/>
</template>

<script setup>
import PageHeader from "/src/vue/components/layout/PageHeader.vue"

const props = defineProps({
    id: String
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>