<script setup lang="ts">
import type { ParsedContent } from '@nuxt/content/dist/runtime/types/index.js';
import { joinURL } from 'ufo'
import { onContentNotFound } from '~/utils/content.js';

const { page, next, prev } = useContent()

onContentNotFound(page)

const formattedDate = computed(() => formatDateStringToHumanReadable(page.value.date))

const route = useRoute()
const linkToCurrentPage = withSiteUrl(route.path)

const links = computed(() => {
  const action = page.value.type === 'podcast' ? 'listened to' : 'checked out'
  const rawShareOnTwitter = `https://twitter.com/intent/tweet?text=I just ${action} "${page.value.title}". Check it out!&url=${linkToCurrentPage.value}&via=TheAlexLichter`
  const shareOnTwitter = encodeURI(rawShareOnTwitter.replace(/#/g, 'No. '))

  const twitterLink = page.value.podcastUrl ?? page.value.videoUrl ?? page.value.slidesUrl ?? linkToCurrentPage.value
  const rawDiscussOnTwitter = `https://twitter.com/search?q=${twitterLink}`

  const editOnGitHub = `https://github.com/manniL/lichter.io-playground/edit/main/content/${page.value._file}`
  return {
    shareOnTwitter,
    discussOnTwitter: encodeURI(rawDiscussOnTwitter),
    editOnGitHub
  }
})

const showCopyingWasSuccessful = ref(false)
async function copyLinkToClipboard() {
  if (showCopyingWasSuccessful.value) {
    return
  }
  await navigator.clipboard.writeText(linkToCurrentPage.value);
  showCopyingWasSuccessful.value = true
  setTimeout(() => {
    showCopyingWasSuccessful.value = false
  }, 5000)
}

// TODO: This should not be necessary. `surround` is buggy?
function isTalkOrPodcast(entry?: ParsedContent): Boolean {
  return Boolean(entry?._path?.startsWith('/speaking/'))
}

defineOgImageComponent('Speaking', {
  title: page.value.title,
  topics: page.value.topics,
  date: formattedDate.value,
  type: page.value.type,
})
</script>
<template>
  <div>
    <AppSection class="bg-gradient-to-b from-black to-zinc-900 !pb-4">
      <AppLinkBack to="/speaking/">Recent Events</AppLinkBack>
      <ParagraphDecoration class="mt-4" />
      <AppParagraph class="mt-4" look="heading" tag="h1">
        {{ page.title }}
      </AppParagraph>
      <div class="flex flex-col md:flex-row gap-4 md:gap-0 justify-between mt-8">
        <ul class="flex flex-col md:flex-row">
          <li v-if="page.eventName">
            <AppLink v-if="page.eventUrl" rel="noindex nofollow"
              class="inline-block underline decoration-white hover:decoration-transparent transition-all mr-1"
              :to="page.eventUrl">
              {{ page.eventName }}
            </AppLink>
            <span v-else class="mr-1">{{ page.eventName }}</span>
            <span v-if="page.location || page.date" class="hidden md:inline-block" aria-hidden>&bull;&nbsp;</span>
          </li>
          <li class="text-sm md:text-base mt-4 md:mt-0" v-if="page.location">
            {{ page.location }}
            <span v-if="page.date" class="hidden md:inline-block" aria-hidden>&bull;&nbsp;</span>
          </li>
          <li class="text-sm md:text-base" v-if="page.date">{{ formattedDate }}</li>
        </ul>
        <ul class="flex gap-8">
          <li v-for="topic in page.topics">
            <AppLink class="hover:underline" :to="`/topics/${topic}`">#{{ topic }}</AppLink>
          </li>
        </ul>
      </div>
      <div class="mt-16">
        <ul class="flex flex-row gap-4 md:gap-8">
          <li v-if="page.slidesUrl">
            <AppLink class="border-b-4 border-white/75 hover:border-white transition-all pr-1 pb-1" :to="page.slidesUrl">
              <Icon name="heroicons:bookmark" /> Check out the slides
            </AppLink>
          </li>
          <li v-if="page.videoUrl">
            <AppLink class="border-b-4 border-white/75 hover:border-white transition-all pr-1 pb-1" :to="page.videoUrl">
              <Icon name="heroicons:play" /> Watch the recording
            </AppLink>
          </li>
          <li v-if="page.podcastUrl">
            <AppLink class="border-b-4 border-white/75 hover:border-white transition-all pr-1 pb-1" :to="page.podcastUrl">
              <Icon name="heroicons:microphone" /> Listen to the podcast
            </AppLink>
          </li>
        </ul>
      </div>
    </AppSection>
    <AppSection class="justify-center bg-zinc-900 pb-8">
      <div>
        <ContentDoc class="prose md:prose-lg lg:prose-xl pt-4" />
      </div>


    </AppSection>
    <AppSection>
      <AppParagraph look="heading" class="mt-16 !text-4xl">Further Recent Events</AppParagraph>
      <div class="flex flex-col gap-8 justify-between mt-16 md:gap-32 md:mt-24">
        <LazySpeakingPreview v-if="isTalkOrPodcast(prev)" :talk="prev" />
        <LazySpeakingPreview v-if="isTalkOrPodcast(next)" :talk="next" />
      </div>
    </AppSection>
  </div>
</template>
