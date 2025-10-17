<template>
    <!-- Services Section -->
    <PageSection variant="primary"
                 :id="props.id">
        <!-- Title -->
        <PageSectionHeader title="这里（社区）有*什么*？"
                           subtitle="Like a chill coffee shop"/>

        <!-- Content -->
        <PageSectionContent>
            <ArticleFeatures>
                <ItemFeature title="每日运动打卡连胜抽咖啡"
                             fa-icon="fa-solid fa-mug-hot"
                             description=""/>

                <ItemFeature title="运动补贴计划"
                             fa-icon="fa-regular fa-star"
                             description=""/>

                <ItemFeature title="全球陌生跑友每天给你一封来自他乡的明信片"
                             fa-icon="fa-solid fa-photo-film"
                             description=""/>

                <ItemFeature title="在这里我们是一群人，一起走"
                             fa-icon="fa-brands fa-gratipay"
                             description=""/>

            </ArticleFeatures>
        </PageSectionContent>
    </PageSection>
</template>

<script setup>
import PageSection from "/src/vue/components/layout/PageSection.vue"
import PageSectionHeader from "/src/vue/components/layout/PageSectionHeader.vue"
import PageSectionContent from "/src/vue/components/layout/PageSectionContent.vue"
import ArticleFeatures from "/src/vue/components/articles/ArticleFeatures.vue"
import ItemFeature from "/src/vue/components/articles/items/ItemFeature.vue"

const props = defineProps({
    id: String
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>