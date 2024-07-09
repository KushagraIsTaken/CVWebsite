<script setup lang="ts">
import { type QueryBuilderParams } from '@nuxt/content/dist/runtime/types/index.js';

definePageMeta({
  documentDriven: false
})

const title = 'Projects - Kushagra Agrawal'
const description = 'Want to upgrade your team\'s skills? I offer various workshops on Vue.js, Nuxt.js, TypeScript, JavaScript, Web Development, Performance, Clean Code and more. Take a look at the list below or contact me for a custom workshop!'

useSeoMeta({
  title,
  description,
})

defineOgImageComponent('Workshop')

const query: QueryBuilderParams = { path: '/workshops', without: ['body', 'excerpt'] }
</script>

<template>
  <AppSection>
    <ParagraphDecoration class="mt-16" />
    <AppParagraph class="mt-4" tag="h1" look="heading">Projects</AppParagraph>
    <AppParagraph class="max-w-3xl mt-8" look="subParagraph">
    I have lead several projects for hackathons such as Smart India Hackathon & Intel Unnati Industrial Training Program. The projects are below :  
    </AppParagraph>
    <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-16 md:gap-8 mt-8">
      <ContentList :query="query" v-slot="{ list }">
        <WorkshopPreview v-for="entry in list" :key="entry._path" :workshop="entry" />
      </ContentList>
    </div>
  </AppSection>
</template>