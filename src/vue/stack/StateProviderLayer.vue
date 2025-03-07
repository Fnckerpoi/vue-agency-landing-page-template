<template>
    <slot/>
</template>

<script setup>
import {provide, ref} from "vue"
import {useSettings} from "/src/composables/settings.js"

const settings = useSettings()

/**
 * Global state CONSTANTS
 **/
const loaderEnabled = settings.getLoaderEnabled()

/**
 * Global state FLAGS
 **/
const currentPageSections = ref([])
const loaderActive = ref(true)
const loaderPageRefreshCount = ref(0)
const loaderSmoothTransitionEnabled = ref(false)
const projectModalTarget = ref(null)
const spinnerActive = ref(false)
const spinnerMessage = ref("")

/**
 * @param {Boolean} enabled
 * @param {String} [message=""]
 */
const setSpinnerEnabled = (enabled, message) => {
    spinnerActive.value = enabled
    spinnerMessage.value = message
}

provide("loaderEnabled", loaderEnabled)

provide("currentPageSections", currentPageSections)
provide("loaderActive", loaderActive)
provide("loaderPageRefreshCount", loaderPageRefreshCount)
provide("loaderSmoothTransitionEnabled", loaderSmoothTransitionEnabled)
provide("projectModalTarget", projectModalTarget)
provide("spinnerActive", spinnerActive)
provide("spinnerMessage", spinnerMessage)

provide("setSpinnerEnabled", setSpinnerEnabled)
</script>

<style lang="scss" scoped>

</style>