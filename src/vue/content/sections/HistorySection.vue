<template>
    <!-- Services Section -->
    <PageSection variant="promo"
                 :id="props.id">
        <!-- Title -->
        <PageSectionHeader title="*曾经我们走过*"
                           subtitle="这里有我们的一切"/>

        <!-- Content -->
        <PageSectionContent>
            <ArticleTimeline>
                <ItemTimelineEntry title="PaoKa成立"
                                   dateStart="2023年4月"
                                   dateEnd=""
                                   image="images/history/history-1.png"
                                   description="1111"
                                   :inverted="true"/>

                <ItemTimelineEntry title="Rapid Growth and Expansion"
                                   dateStart="2010"
                                   dateEnd="2013"
                                   image="images/history/history-2.png"
                                   description="By 2013, our agency's reputation for quality services led to rapid growth, prompting us to expand our team and open a new office to better serve clients worldwide. We embraced opportunities for expansion."
                                   :inverted="false"/>

                <ItemTimelineEntry title="Diversification and Specialization"
                                   dateStart="2013"
                                   dateEnd="2019"
                                   image="images/history/history-3.png"
                                   description="In 2017, we diversified our offerings, adding web design, SEO, social media management, and branding services, positioning ourselves as a comprehensive digital solutions provider. We became a one-stop-shop for clients."
                                   :inverted="true"/>

                <ItemTimelineEntry title="Celebrating a Decade of Success"
                                   dateStart="2020"
                                   dateEnd="2022"
                                   image="images/history/history-4.png"
                                   description="Proudly celebrating our 10th anniversary, our agency's decade-long journey is defined by innovation, exceptional service, and strong client relationships, empowering businesses through technology and creativity. We achieved remarkable success."
                                   :inverted="false"/>

                <ItemTimelineEntry title="Planning for New Stuff"
                                   dateStart="2023"
                                   dateEnd="Now"
                                   image="images/history/history-5.png"
                                   description="As we continue to grow and evolve, we invite talented individuals, partners, and clients to join us in shaping the future of digital innovation and making a meaningful impact together. We are excited for what's to come."
                                   :inverted="true"/>
            </ArticleTimeline>
        </PageSectionContent>
    </PageSection>
</template>

<script setup>
import PageSection from "/src/vue/components/layout/PageSection.vue"
import PageSectionHeader from "/src/vue/components/layout/PageSectionHeader.vue"
import PageSectionContent from "/src/vue/components/layout/PageSectionContent.vue"
import ArticleTimeline from "/src/vue/components/articles/ArticleTimeline.vue"
import ItemTimelineEntry from "/src/vue/components/articles/items/ItemTimelineEntry.vue"

const props = defineProps({
    id: String
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>