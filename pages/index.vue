<script setup lang="ts">
import type { ArticlePreview, TalkPreview } from '~/types.js';

definePageMeta({
  documentDriven: false
})

const description = `I am Kushagra Agrawal, a dynamic and dedicated Computer Engineering student with a passion for catalyzing research organizations through innovative problem-solving and practical implementation.          
`

useSeoMeta({
  title: 'Kushagra Agrawal',
  ogTitle: 'Kushagra Agrawal - Student Researcher',
  description,
})

defineOgImageComponent('Main')

const { data: articles } = useAsyncData('latest-articles', () => queryContent<ArticlePreview>('/articles').sort({
  dateModified: -1,
  datePublished: -1
}).without(['body', 'excerpt']).limit(4).find())

const { data: talks } = useAsyncData('latest-speaking', () => queryContent<TalkPreview>('/speaking/').sort({
  date: -1
}).without(['body', 'excerpt']).limit(5).find())

const { data: workshops } = useAsyncData('latest-workshops', () => queryContent('/workshops/').sort({
  onStartPage: 1
}).without(['body', 'excerpt']).limit(3).find())
</script>

<template>
  <div>
    <AppSection>
      <div class="md:flex md:flex-row items-center">
        <div class="mt-8 md:mt-0 md:w-3/5 md:flex-1">
          <div class="flex gap-8 -mx-4 md:mx-0">
            <div class="flex w-1/2 md:w-full items-center">
              <AppParagraph tag="h1" look="superHeading"
                class="flex flex-col sm:justify-start font-mono mt-8 md:mt-0 ml-4 md:ml-0">
                <span>Learn</span>
                <span>Analyze</span>
                <span>Research</span>
              </AppParagraph>
            </div>
            <div class="md:hidden w-1/2">
              <NuxtPicture format="avif,webp,png" width="358" height="468" densities="x1 x2" placeholder :img-attrs="{ class: 'z-20 relative' }"
                src="img/kush-main.png" alt="Photo of Kushagra Agrawal" />
            </div>
          </div>
          <AppParagraph look="subParagraph" class="mt-8">
            I am Kushagra Agrawal, a dynamic and dedicated Computer Engineering student with a passion for catalyzing research organizations through innovative problem-solving and practical implementation.          
            </AppParagraph>
          <AppParagraph look="subParagraph" class="mt-6">
            I specialize in Machine Learning, Deep Learning, Transformers, and Artificial Intelligence. I am committed to giving back to society with the skills I learn. </AppParagraph>
          <div class="mt-8 flex">
            <AppButton to="https://topmate.io/kushagra_agrawal" look="secondary">Schedule <span class="hidden sm:inline">Meeting</span></AppButton>
            <AppButton to="/about/" look="secondary">About <span class="hidden sm:inline">me</span></AppButton>
          </div>

        </div>
        <div class="w-1/2 md:w-2/5 md:flex-1 h-full hidden md:flex justify-end items-center md:ml-32 md:mt-8">
          <NuxtPicture format="avif,webp,png" width="544" height="710" densities="x1 x2" placeholder :img-attrs="{ class: 'z-20 relative' }"
            src="img/kush-main.png" alt="Photo of Kushagra Agrawal" />
        </div>
      </div>
      <ContentDivider class="mt-16 md:-mt-10" />
    </AppSection>
    <AppSection class="my-32">
      <div class="flex flex-col gap-16 md:gap-8 md:flex-row justify-around">
        <LazyServicePreview icon="mdi:lightbulb-on-outline" title="Research" to="/consulting">
        Actively contributing to the scientific community as a researcher and reviewer through research and reviewing articles, book chapters, and magazines        </LazyServicePreview>
        <LazyServicePreview icon="ph:chalkboard-teacher-light" title="Learn" to="/workshops">
          An active learner in the field of Machine Learning, Deep Learning, Transformers, Vision Transformers, LLMs and Cloud Services
        </LazyServicePreview>
        <LazyServicePreview icon="ph:microphone" title="Public speaking" to="/speaking">
          I love to share my knowledge and experience with the community.
          I speak at conferences and meetups, and I am always open to new opportunities.
        </LazyServicePreview>
      </div>
      <ContentDivider class="mt-32" anchor="left" />
    </AppSection>
    <AppSection class="mt-48 md:mt-32">
      <LazyParagraphDecoration />
      <AppParagraph class="mr-8 mt-4" tag="h2" look="heading">
        Projects
      </AppParagraph>
      <div class="flex flex-col gap-8 md:gap-0 md:flex-row justify-between">
        <AppParagraph look="subParagraph" class="mt-8 max-w-xl">
        I love taking the lead on projects and have successfully spearheaded several initiatives. Below are some of the projects I have led:
        </AppParagraph>
        <div>
          <AppButton to="/workshops/" look="secondary">Discover All Projects </AppButton>
        </div>
      </div>
      <div class="flex flex-col md:flex-row gap-16 md:gap-8 justify-around mt-8">
        <LazyWorkshopPreview class="flex-1" v-for="workshop in workshops" :workshop="workshop" />
      </div>
      <ContentDivider class="mt-14" />
    </AppSection>
    <AppSection class="bg-zinc-900">
      <LazyParagraphDecoration class="mt-16" />
      <AppParagraph class="mr-8 mt-4" tag="h2" look="heading">
        Publications
      </AppParagraph>
      <div class="flex flex-col gap-8 md:gap-0 md:flex-row justify-between">
        <AppParagraph look="subParagraph" class="mt-8 max-w-xl">
          I am an active contibutor to the scientific community. I write articles, conference papers, journal papers, book chapters and much more. I am open to collaboration.
          Have a look at my latest publications below.
        </AppParagraph>
        <div>
          <AppButton to="/articles" look="secondary" secondary-after-bg="bg-zinc-900">View all publications</AppButton>
        </div>
      </div>
      <div class="grid md:grid-cols-2 gap-12 justify-around mt-8">
        <ArticlePreview v-for="article in articles" :key="article._id" :article="article" />
      </div>
      <div class="flex md:justify-end mt-8">
        <AppButton to="/articles" look="secondary" secondary-after-bg="bg-zinc-900">View all publications</AppButton>
      </div>
      <ContentDivider anchor="left" class="mt-14" />
    </AppSection>
    <AppSection>
      <LazyParagraphDecoration class="mt-16" />
      <AppParagraph class="mr-8 mt-4" tag="h2" look="heading">
        Recent Events
      </AppParagraph>
      <div class="flex flex-col gap-8 md:gap-0 md:flex-row justify-between">
        <AppParagraph look="subParagraph" class="mt-8 max-w-xl">
          I love to take time off from my daily schedule to connect with people in different workshops, summer schools, conferences and much more.
        </AppParagraph>
        <div>
          <AppButton to="/speaking/" look="secondary">All Revent Events</AppButton>
        </div>
      </div>
      <div class="flex flex-col space-y-8 mt-8">
        <LazySpeakingPreview v-for="talk in talks" :key="talk._id" :talk="talk" />
      </div>
      <div class="flex md:justify-end mt-16">
        <AppButton to="/speaking/" look="secondary">All Revent Events</AppButton>
      </div>
    </AppSection>
  </div>
</template>