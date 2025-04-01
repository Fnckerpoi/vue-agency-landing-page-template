<template>
    <ActivitySpinner :visible="Boolean(spinnerActive)"
                     :message="String(spinnerMessage)"/>

    <Loader v-if="loaderEnabled"
            :visible="Boolean(loaderActive)"
            :refresh-count="Number(loaderPageRefreshCount)"
            :smooth-transition-enabled="Boolean(loaderSmoothTransitionEnabled)"
            @ready="_onLoaderMounted"
            @completed="_onLoaderCompleted"/>

    <slot v-if="didMountPreloader"/>
</template>

<script setup>
import {inject, ref} from "vue"
import ActivitySpinner from "/src/vue/components/loaders/ActivitySpinner.vue"
import Loader from "/src/vue/components/loaders/Loader.vue"

const loaderEnabled = inject("loaderEnabled")
const loaderActive = inject("loaderActive")
const loaderPageRefreshCount = inject("loaderPageRefreshCount")
const loaderSmoothTransitionEnabled = inject("loaderSmoothTransitionEnabled")
const spinnerActive = inject("spinnerActive")
const spinnerMessage = inject("spinnerMessage")

const didMountPreloader = ref(!loaderEnabled)

const _onLoaderMounted = () => {
    didMountPreloader.value = true
}

const _onLoaderCompleted = () => {
    loaderActive.value = false
}
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>