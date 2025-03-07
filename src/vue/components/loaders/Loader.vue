<template>
    <!-- Loader Wrapper -->
    <div v-if="visible && currentStep"
         id="foxy-loader"
         class="foxy-loader"
         :class="{
            'foxy-loader-tween-in': currentStep === Steps.WILL_ENTER,
            'foxy-loader-tween-out': currentStep === Steps.LEAVING
         }">
        <!-- Loader Content -->
        <div class="foxy-loader-content">
            <ImageView src="images/logo/agency-logo-small.png"
                       alt="Logo"
                       class="image-view-logo"
                       :class="{
                          'image-view-logo-animated': currentStep >= Steps.ANIMATING_LOGO
                       }"
                       @completed="_onLogoLoaded"
                       :spinner-enabled="false"/>

            <div class="foxy-loader-progress-display"
                 :class="{
                    'foxy-loader-progress-display-hidden': currentStep <  Steps.ANIMATING_PROGRESS
                 }">
                <p class="percentage text-2"
                   v-html="`${percentage}%`"/>

                <ProgressBar class="foxy-loader-progress-bar"
                             :percentage="percentage"/>
            </div>
        </div>
    </div>
</template>

<script setup>
import {onMounted, watch, ref} from "vue"
import {useUtils} from "/src/composables/utils.js"
import {useLayout} from "/src/composables/layout.js"
import {useScheduler} from "/src/composables/scheduler.js"
import ImageView from "/src/vue/components/generic/ImageView.vue"
import ProgressBar from "/src/vue/components/widgets/ProgressBar.vue"

const utils = useUtils()
const layout = useLayout()
const scheduler = useScheduler()

const props = defineProps({
    visible: Boolean,
    smoothTransitionEnabled: Boolean
})

const Steps = {
    NONE: 0,
    WILL_ENTER: 1,
    ENTERING: 2,
    LOADING_LOGO: 3,
    ANIMATING_LOGO: 4,
    ANIMATING_PROGRESS: 5,
    WAITING_FOR_COMPLETION: 6,
    LEAVING: 7
}

const emit = defineEmits(['mounted', 'completed'])

const schedulerTag = "loader"
const didLoadLogo = ref(false)
const currentStep = ref(Steps.NONE)
const percentage = ref(0)

onMounted(() => {
    emit('mounted')
    scheduler.clearAllWithTag(schedulerTag)
    _performTransition()
})

watch(() => props.visible, () => {
    scheduler.clearAllWithTag(schedulerTag)
    _performTransition()
})

const _onLogoLoaded = () => {
    didLoadLogo.value = true
}

const _performTransition = () => {
    if(!props.visible)
        return

    percentage.value = 0
    currentStep.value = Steps.NONE

    if(props.smoothTransitionEnabled)
        _executeEnteringStep()
    else
        _executeAnimatingLogoStep()
}

const _executeEnteringStep = () => {
    currentStep.value = Steps.WILL_ENTER

    scheduler.schedule(() => {
        currentStep.value = Steps.ENTERING
    }, 30, schedulerTag)

    scheduler.schedule(() => {
        _executeAnimatingLogoStep()
    }, 350, schedulerTag)
}

const _executeAnimatingLogoStep = () => {
    currentStep.value = Steps.LOADING_LOGO
    layout.setBodyScrollEnabled(false)

    if(!didLoadLogo.value) {
        scheduler.schedule(() => {
            _executeAnimatingLogoStep()
        }, 100, schedulerTag)
        return
    }

    currentStep.value = Steps.ANIMATING_LOGO
    scheduler.schedule(() => {
        _executeAnimatingProgressStep()
    }, 300, schedulerTag)
}

const _executeAnimatingProgressStep = () => {
    currentStep.value = Steps.ANIMATING_PROGRESS
    scheduler.schedule(() => {
        _executeWaitingForCompletionStep()
    }, 300, schedulerTag)
}

const _executeWaitingForCompletionStep = () => {
    currentStep.value = Steps.WAITING_FOR_COMPLETION

    let dt = 0
    const step = 1000 / 30
    scheduler.interval(() => {
        const imageElements = document.querySelectorAll(".image")
        const imageLoadProgress = {loaded: 0, total: 0}
        Array.from(imageElements).map(item => {
            imageLoadProgress.total++
            if(item.getAttribute('load-status') !== "loading")
                imageLoadProgress.loaded++
        })

        dt += step

        const percentageFromDt = dt*step/100
        const percentageFromProgress = imageLoadProgress.total ?
            imageLoadProgress.loaded*100/imageLoadProgress.total :
            0

        percentage.value = Math.round(Math.min(percentageFromDt, percentageFromProgress))
        if(percentage.value >= 100 || dt > 5000) {
            _onLoadingComplete()
        }
    }, step, schedulerTag)
}

const _onLoadingComplete = () => {
    scheduler.schedule(() => {
        percentage.value = 100
        _executeLeavingStep()
    }, 300, schedulerTag)
}

const _executeLeavingStep = () => {
    currentStep.value = Steps.LEAVING
    layout.setBodyScrollEnabled(true)
    scheduler.schedule(() => {
        emit('completed')
    }, 900, schedulerTag)
}
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

div.foxy-loader {
    position: fixed;
    z-index: 100;
    user-select: none;

    display: flex;
    justify-content: center;
    align-items: center;

    background-color: $dark;
    width: 100vw;
    height: 125vh;
    height: 125svh;
    top: -12.5vh;
    top: -12.5svh;
    transition: opacity 0.3s ease-in;

    &-tween-in {
        opacity: 0;
        transition: none!important;
        user-select: none;
        pointer-events: none;
    }

    &-tween-out {
        top: -125vh;
        transition: 1.2s top cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }
}

div.foxy-loader-content {
    color: $text-normal-contrast;
    text-align: center;
    padding-bottom: 5rem;
}

div.image-view-logo {
    width: 60px;
    height: 60px;
    z-index: 10;
    opacity: 0;

    &-animated {
        animation: popIn 0.3s ease-out forwards;
    }
}

div.foxy-loader-progress-display {
    margin-top: 5px;
    overflow: hidden;
    z-index: 5;
    transition: 0.3s all ease-out;

    &-hidden {
        opacity: 0;
        margin-top: -30px;
    }

    p {
        color: $text-normal-contrast;
        margin-bottom: 5px;
    }

    .foxy-loader-progress-bar {
        max-width: 55px;
        margin: 0 auto;
    }
}

@keyframes popIn {
    from {
        opacity:0;
        transform: scale(0.2) translateY(-100%);
    }
    to {
        opacity:1
    }
}
</style>