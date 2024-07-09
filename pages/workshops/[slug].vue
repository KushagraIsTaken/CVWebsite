<script setup lang="ts">
import { onContentNotFound } from '~/utils/content.js';

const { page: workshop } = useContent()

useSeoMeta({
  title: () => workshop.value.title,
  description: () => workshop.value.description,  
  ogTitle: () => workshop.value.title,
  ogDescription: () => workshop.value.description,
})

onContentNotFound(workshop)

defineOgImageComponent('Workshop', {
  title: workshop.value.title,
  time: workshop.value.time,
})

</script>

<template>
  <div>
    <AppSection class="bg-gradient-to-b from-black to-zinc-900 !pb-4">
      <AppLinkBack to="/workshops/">All Workshops</AppLinkBack>
      <ParagraphDecoration class="mt-4" />
      <AppParagraph class="mt-4" look="heading" tag="h1">
        {{ workshop.title }}
      </AppParagraph>
    </AppSection>
    <AppSection class="bg-zinc-900 !pb-0" inner-class="border-b border-zinc-800">
      <div class="md:grid grid-cols-2 justify-center gap-8 pb-16">
        <div>
          <div class="prose md:prose-lg lg:prose-xl pt-0.5">
            <ContentDoc />
          </div>
        </div>
      </div>
    </AppSection>
  </div>
</template>