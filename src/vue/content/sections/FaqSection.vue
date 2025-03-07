<template>
    <!-- About Section -->
    <PageSection variant="default"
                 :id="props.id">
        <!-- Title -->
        <PageSectionHeader title="Questions and *Answers*"
                           subtitle="Quick answers to your queries!"/>

        <!-- Content -->
        <PageSectionContent>
            <ArticleFaq>
                <ItemFaqQuestion question="How do I customize the content of the template?"
                                 answer="To customize the content, you'll need to modify the <i>agency.json</i> and the <i>sections.json</i> files, which are located in the <i>data</i> folder within the <i>public</i> directory. These JSON files contain the necessary data for the template, allowing you to change texts, images, links, and other elements as per your requirements. Make sure to follow the provided structure to avoid any formatting issues. Additionally, if you need to add new sections or make more extensive changes, you may need to work with the Vue components and other files within the template's structure."/>

                <ItemFaqQuestion question="Can I expect the template to be responsive and work well on mobile devices?"
                                 answer="Absolutely! The template is designed with responsiveness in mind, ensuring that it adapts to various screen types and sizes, including mobile devices. The use of responsive design techniques like media queries and flexible layout ensures that the template looks and functions well on smartphones, tablets, and other mobile devices. During customization, make sure to preview the template on different screen sizes and devices to ensure it displays correctly. If you encounter any issues, you can adjust the CSS styles or layout accordingly to improve the mobile experience further."/>

                <ItemFaqQuestion question="How can I enable the functionality of the contact form?"
                                 answer="Integrating the contact form requires implementing your own server-side logic. Please note that the current template only includes the client-side implementation. You'll need to set up a backend server to handle form submissions, process data, and send emails or perform other actions as needed. Ensure that the server-side code is secure to prevent potential security vulnerabilities. On the frontend, you can link the form submission to your backend endpoints using JavaScript. Keep in mind that specific steps may vary based on your backend technology and preferences."/>

                <ItemFaqQuestion question="What steps should I follow to add a new section to the theme?"
                                 answer="Adding a new section to the theme involves a few steps. First, create a new Vue component for it in the <i>sections</i> folder. Use the existing components as a reference to maintain consistency with the template's design and functionality. Next, within the <i>public/data/sections.json</i> file, create an item for the new section, where you can define all the necessary data such as texts, links, and other information. After completing these steps, your new section should be fully integrated into the theme."/>
            </ArticleFaq>
        </PageSectionContent>

        <!-- Footer -->
        <PageSectionFooter title="*Save time* with Foxy!"
                           description="Foxy beautifully and intuitively extends the Vue and Bootstrap frameworks making it easy to build your next project!"
                           :include-divider="false"
                           :description-text-class="`text-3`"
                           button-label="Download Now!"
                           button-fa-icon="fa-solid fa-download"
                           button-url="https://github.com/ryanbalieiro/vue-agency-landing-page-template"/>
    </PageSection>
</template>

<script setup>
import PageSection from "/src/vue/components/layout/PageSection.vue"
import PageSectionHeader from "/src/vue/components/layout/PageSectionHeader.vue"
import PageSectionContent from "/src/vue/components/layout/PageSectionContent.vue"
import PageSectionFooter from "/src/vue/components/layout/PageSectionFooter.vue"
import ArticleFaq from "/src/vue/components/articles/ArticleFaq.vue"
import ItemFaqQuestion from "/src/vue/components/articles/items/ItemFaqQuestion.vue"

const props = defineProps({
    id: String
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";
</style>