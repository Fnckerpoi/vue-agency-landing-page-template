<template>
    <ActivitySpinner :visible="Boolean(spinnerActive)"
                     :message="String(spinnerMessage)"/>

    <Loader v-if="loaderEnabled"
            :visible="Boolean(loaderActive)"
            :refresh-count="Number(loaderPageRefreshCount)"
            :smooth-transition-enabled="Boolean(loaderSmoothTransitionEnabled)"
            @rendered="_onLoaderRendered"
            @ready="_onLoaderReady"
            @completed="_onLoaderCompleted"/>

    <slot v-if="isReady"/>
</template>

<script setup>
import {inject, provide, ref} from "vue"
import ActivitySpinner from "/src/vue/components/loaders/ActivitySpinner.vue"
import Loader from "/src/vue/components/loaders/Loader.vue"

const loaderEnabled = inject("loaderEnabled")
const loaderActive = inject("loaderActive")
const loaderPageRefreshCount = inject("loaderPageRefreshCount")
const loaderSmoothTransitionEnabled = inject("loaderSmoothTransitionEnabled")
const spinnerActive = inject("spinnerActive")
const spinnerMessage = inject("spinnerMessage")

const isReady = ref(!loaderEnabled)
const isLoaderAnimating = ref(loaderEnabled)

const _onLoaderRendered = () => {
    isLoaderAnimating.value = true
}

const _onLoaderReady = () => {
    isReady.value = true
    isLoaderAnimating.value = false
}

const _onLoaderCompleted = () => {
    loaderActive.value = false
}

provide("isLoaderAnimating", isLoaderAnimating)
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>