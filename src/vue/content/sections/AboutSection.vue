<template>
    <!-- 关于部分 -->
    <PageSection variant="primary" :id="props.id">
        <!-- 标题 -->
        <PageSectionHeader title="*About* PAOKA" subtitle="来了解我们是一个怎样的社区" />
        <!-- 内容 -->
        <PageSectionContent>
            <!-- 关于模板 -->
            <ArticleInfoBlock :image="[`images/portfolio/daka1.png`,`images/portfolio/daka2.png`]" :paragraphs="[
                `<b>跑咖</b> PaoKa | 每天十分钟，用脚步连接世界 🏃🌍.`,
                `跑咖是一个以「坚持运动」为核心理念的全球打卡社区，让想要保持健康、每天运动的朋友在这里集合、打卡、相互激励。`,
                `在这里，你无需刻意寒暄或强行社交，我们更看重的是轻社交的弱连接陪伴感：`,
                `每天抽出至少十分钟健走或跑步，完成一次简单的打卡，你就能拆开一枚特别的「运动社交盲盒」🎁。盲盒中可能是一张由全球陌生跑友拍摄并投稿分享的风景照片，也可能是一张能真实兑换的咖啡券 ☕️，用日常的小惊喜奖励你的坚持。偶尔，你还会解锁来自特殊地点、特别意义的稀有款明信片📍。`,
                `你也能成为盲盒的贡献者，如果愿意分享你走过的美好风景，也会有陌生的全球跑友因为你的分享多一份坚持下去的动力。`,
                `社区首页的「流水打卡墙」，每天滚动展示全球跑友的里程与坚持 🏃‍♀️🏃‍♂️。你不必主动聊天，只需轻轻一个点赞或表情回应，就能感受到「即便独跑，也有人一起跑」的默契陪伴。`,
                `无论你是刚起步的新手，还是追求进阶的跑者，在这里都能找到适合你的节奏与共鸣。科学研究显示，每天健走十分钟，就能显著改善心肺健康，提升精力和情绪状态。`,
            ]" />
        </PageSectionContent>


        <!-- 页脚 -->
        <PageSectionFooter title="加入我们的社区"
            description="欢迎加入跑咖，用每天十分钟的坚持，与全球伙伴一起用脚步丈量城市；也用日常打卡，建立柔软而坚韧的社交连接 🌟。" :include-divider="true"
            button-label="Join Now!" button-fa-icon="fa-brands fa-discord"
            button-url="https://discord.com/invite/paoka" />
    </PageSection>
</template>

<script setup>
import BackgroundPromo from "/src/vue/components/layout/BackgroundPromo.vue"
import PageSection from "/src/vue/components/layout/PageSection.vue"
import PageSectionHeader from "/src/vue/components/layout/PageSectionHeader.vue"
import PageSectionContent from "/src/vue/components/layout/PageSectionContent.vue"
import PageSectionFooter from "/src/vue/components/layout/PageSectionFooter.vue"
import ArticleInfoBlock from "/src/vue/components/articles/ArticleInfoBlock.vue"

const props = defineProps({
    id: String
})
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";


</style>