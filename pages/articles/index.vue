<script setup lang="ts">
import type { QueryBuilderParams } from '@nuxt/content/dist/runtime/types'
import type { Article } from '~/types.js';

definePageMeta({
  documentDriven: false
})

// TODO: Remove type casting after https://github.com/nuxt/content/pull/2156 landed

const query: QueryBuilderParams = { path: '/articles', sort: [{ dateModified: -1, datePublished: -1 }] }

const title = 'Publications - Kushagra Agrawal'
const description = 'I am an active contibutor to the scientific community. I write articles, conference papers, journal papers, book chapters and much more. I am open to collaboration.'

useSeoMeta({
  title,
  description,
})

defineOgImageComponent('Article')
</script>

<template>
  <AppSection>
    <ParagraphDecoration class="mt-16" />
    <AppParagraph class="mt-4" tag="h1" look="heading">Publications</AppParagraph>
    <AppParagraph class="max-w-3xl mt-8" look="subParagraph">
    I am an active contibutor to the scientific community. I write articles, conference papers, journal papers, book chapters and much more. I am open to collaboration.
    </AppParagraph>
    <div class="space-y-8 md:space-y-0 md:grid grid-cols-2 gap-12 justify-around mt-8">
      <ContentList :query="query" v-slot="{ list }">
        <ArticlePreview v-for="entry in list" :key="entry._path" :article="(entry as Article)" />
      </ContentList>
    </div>
  </AppSection>
</template>