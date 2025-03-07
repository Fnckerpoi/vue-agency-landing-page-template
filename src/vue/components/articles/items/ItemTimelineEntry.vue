<template>
    <li class="foxy-timeline-item"
        :class="trailing ? `foxy-timeline-item-trailing` : ``">
        <!-- Image -->
        <div class="foxy-timeline-image-wrapper"
             :class="trailing ? `foxy-timeline-image-wrapper-sm` : ``">
            <ImageView v-if="props.image"
                       :src="props.image"
                       :alt="props.title"/>
        </div>

        <!-- Panel -->
        <div v-if="title || description"
             class="foxy-timeline-panel"
             :class="{'foxy-timeline-panel-inverted': inverted}">
            <div class="heading">
                <!-- Title -->
                <h3 class="mb-1"
                    v-html="parsedTitle"/>

                <!-- Date -->
                <span v-if="date" class="badge bg-light text-dark text-2 mb-3 mt-1">
                    <i class="fa fa-calendar-check me-1"/>
                    {{ props.date }}
                </span>
            </div>

            <div v-if="description" class="content">
                <!-- Description -->
                <p class="text-muted text-4"
                   v-html="parsedDescription"/>
            </div>
        </div>
    </li>
</template>

<script setup>
import {useUtils} from "/src/composables/utils.js"
import ImageView from "/src/vue/components/generic/ImageView.vue"
import {computed} from "vue"

const utils = useUtils()

const props = defineProps({
    title: String,
    date: String,
    image: String,
    description: String,
    inverted: Boolean,
    trailing: Boolean
})

const parsedTitle = computed(() => {
    return utils.parseTitle(props.title)
})

const parsedDescription = computed(() => {
    return utils.parseTitle(props.description)
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

li.foxy-timeline-item {
    position: relative;
    min-height: var(--min-item-height);
    margin-bottom: calc(var(--min-item-height)/3);

    &:after,
    &:before {
        display: table;
        content: " ";
    }

    &:after {
        clear: both;
    }
}

li.foxy-timeline-item-trailing {
    min-height: calc(var(--min-item-height)/3);
    margin-bottom: 0;
}

div.foxy-timeline-image-wrapper {
    position: absolute;
    left: calc(var(--line-position) - var(--image-dimensions)/2);
    width: var(--image-dimensions);
    height: var(--image-dimensions);
    z-index: 5;

    border: 7px solid $light-2;
    border-radius: 100%;
    overflow: hidden;
    background-color: $light-4;

    &-sm {
        width: calc(var(--image-dimensions)/3);
        height: calc(var(--image-dimensions)/3);
        left: calc(var(--line-position) - var(--image-dimensions)/6);
        top: calc(var(--image-dimensions)/6);
        border-width: 3px;
    }

    div.image-view {
        width: 100%;
        height: 100%;
    }
}

div.foxy-timeline-panel {
    position: relative;
    float: right;
    text-align: left;
    width: var(--min-item-width);
    padding: var(--item-padding);

    &-inverted {
        float: var(--inverted-float);
        text-align: var(--inverted-align);
    }
}
</style>