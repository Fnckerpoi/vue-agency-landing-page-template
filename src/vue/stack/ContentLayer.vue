<template>
    <!-- Main Content -->
    <slot/>

    <!-- Modals -->
    <ProjectModal :project="projectModalTarget"
                  @close="_onProjectModalClosed"/>
</template>

<script setup>
import {inject} from "vue"
import {useRouter} from "vue-router"
import ProjectModal from "/src/vue/components/projects/ProjectModal.vue"

const router = useRouter()

const loaderEnabled = inject("loaderEnabled")
const loaderActive = inject("loaderActive")
const loaderSmoothTransitionEnabled = inject("loaderSmoothTransitionEnabled")
const projectModalTarget = inject("projectModalTarget")

router.beforeEach((to, from, next) => {
    if(from.name === to.name) {
        next()
        return
    }

    if(!loaderEnabled) {
        _resetScroll()
        next()
        return
    }

    loaderActive.value = true
    loaderSmoothTransitionEnabled.value = from && to && from.path !== to.path
    setTimeout(() => {
        _resetScroll()
        next()
    }, 350)
})

const _resetScroll = () => {
    window.scrollTo({
        top: 0,
        behavior: "instant"
    })
}

const _onProjectModalClosed = () => {
    projectModalTarget.value = null
}
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>