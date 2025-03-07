<template>
    <article class="foxy-info-block-faq">
        <!-- Upper Divider -->
        <hr class="foxy-info-block-faq-divider mt-0 mb-4 pb-1 pg-lg-0 mb-lg-4">

        <!-- Row -->
        <div class="row">
            <template v-if="$slots.default">
                <div v-for="(child, index) in $slots.default()" class="col-12 col-lg-6">
                    <component :is="child" />
                </div>
            </template>
        </div>

        <!-- Bottom Divider -->
        <hr class="foxy-info-block-faq-divider mt-0 mt-lg-2 mb-4 pb-2 pb-md-3">
    </article>
</template>

<script setup>
const props = defineProps({})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

hr.foxy-info-block-faq-divider {
    opacity: 0.1;
}
</style>