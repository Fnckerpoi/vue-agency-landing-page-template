<template>
    <!-- 主要内容 -->
    <slot v-if="shouldSlot"/>

    <!-- 莫代尔 -->
    <ProjectModal :project="projectModalTarget"
                  @close="_onProjectModalClosed"/>
</template>

<script setup>
import {computed, inject, onMounted, watch} from "vue"
import {useRouter} from "vue-router"
import ProjectModal from "/src/vue/components/projects/ProjectModal.vue"
import {useUtils} from "/src/composables/utils.js"

const router = useRouter()
const utils = useUtils()

const loaderEnabled = inject("loaderEnabled")
const loaderActive = inject("loaderActive")
const loaderPageRefreshCount = inject("loaderPageRefreshCount")
const loaderSmoothTransitionEnabled = inject("loaderSmoothTransitionEnabled")
const projectModalTarget = inject("projectModalTarget")
const LoaderAnimationStatus = inject("LoaderAnimationStatus")
const loaderAnimationStatus = inject("loaderAnimationStatus")

const shouldSlot = computed(() => {
    return !loaderEnabled ||
        loaderAnimationStatus.value === LoaderAnimationStatus.TRACKING_PROGRESS ||
        loaderAnimationStatus.value === LoaderAnimationStatus.LEAVING
})

/**
 * @description 该挂钩可用于报告对外部分析服务的访问。
 *在这里，您可以集成 Google Analytics、Mixpanel 或您自己的自定义分析实施。
 */
onMounted(() => {
    // 用您自己的分析服务替换下面的实现...

    fetch("https://ryanbalieiro.com/api/analytics/mock", {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
            params: {
                url: utils.getRootLocation(),
                template_id: "foxy-agency"
            }
        })
    })
})

watch(() => loaderAnimationStatus.value, () => {
    if(loaderAnimationStatus.value === LoaderAnimationStatus.LEAVING) {
        const hash = window.location.hash
        const element = hash ?
            document.querySelector(hash) :
            null

        if(!element || !loaderEnabled) {
            window.scrollTo({top: 0, behavior: "instant"})
            return
        }

        element.scrollIntoView({behavior: "smooth"})
    }
})

router.beforeEach((to, from, next) => {
    if(from.name === to.name || !loaderEnabled) {
        next()
        return
    }

    const shouldIgnorePreloader = to.matched && to.matched.length ?
        !to.matched[0].props.default['shouldAlwaysPreload'] :
        false

    if(shouldIgnorePreloader) {
        next()
        window.scrollTo({top: 0, behavior: "instant"})
        return
    }

    loaderActive.value = true
    const isDifferentRoute = from && to && from.path !== to.path
    const isDifferentRouteName = from && to && from.name !== to.name

    loaderPageRefreshCount.value = isDifferentRouteName ?
        loaderPageRefreshCount.value + 1 :
        loaderPageRefreshCount.value

    loaderSmoothTransitionEnabled.value = isDifferentRoute

    setTimeout(() => {
        next()
    }, 850)
})

router.afterEach((to, from) => {
    const isDifferentRoute = from && to && from.path !== to.path
    if(!isDifferentRoute)
        return

    window.scrollTo({top: 0, behavior: "smooth"})
})

const _onProjectModalClosed = () => {
    projectModalTarget.value = null
}
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>