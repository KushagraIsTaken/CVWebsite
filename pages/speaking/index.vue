<script setup lang="ts">
import type { QueryBuilderParams } from '@nuxt/content/dist/runtime/types'
import type { Talk } from '~/types.js';

// TODO: Remove type casting after https://github.com/nuxt/content/pull/2156 landed

definePageMeta({
  documentDriven: false
})

const title = 'Events - Kushagra Agrawal'
const description = ``

useSeoMeta({
  title,
  description,
})

defineOgImageComponent('Speaking', {
  title: 'Talks and Podcasts'
})

const query: QueryBuilderParams = { path: '/speaking', sort: [{ date: -1 }], without: ['body', 'excerpt'] }
</script>

<template>
  <AppSection>
    <ParagraphDecoration class="mt-16" />
    <AppParagraph class="mt-4" tag="h1" look="heading">Recent Events</AppParagraph>
    <AppParagraph class="max-w-3xl mt-8" look="subParagraph">
    I actively engage in various conferences, seminars, meetups, summerschools to network and engage with people.
    </AppParagraph>
    <div class="space-y-8 mt-8">
      <ContentList :query="query" v-slot="{ list }">
        <SpeakingPreview v-for="entry in list" :key="entry._path" :talk="(entry as Talk)" />
      </ContentList>
    </div>
  </AppSection>
</template>