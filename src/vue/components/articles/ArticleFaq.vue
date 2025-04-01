<template>
    <article class="foxy-info-block-faq">
        <!-- Row -->
        <div class="row gy-3 gy-xl-4 py-2">
            <template v-if="$slots.default">
                <div v-for="(child, index) in $slots.default()" class="col-12 col-lg-6">
                    <component :is="child" />
                </div>
            </template>
        </div>
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