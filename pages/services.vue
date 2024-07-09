<script setup lang="ts">
definePageMeta({
  documentDriven: false
})

const title = 'Career Objectives - Kushagra Agrawal'
const description = 'Take a look at the services I offer, including web engineering consulting, workshops for various topics and more.'

useSeoMeta({
  title,
  description,
})

defineOgImageComponent('General')
</script>

<template>
  <div>
    <AppSection>
      <ParagraphDecoration />
      <AppParagraph look="heading" class="mt-4" tag="h1">Career Objectives</AppParagraph>
      <div class="flex flex-col items-center md:flex-row my-16 gap-16">
        <ServicePreview class="max-w-xl bg-zinc-900 p-8" icon="mdi:lightbulb-on-outline" title="Sustainability">
        Leveraging AI for sustainability, innovating solutions that address environmental challenges through data-driven insights and technology integration, fostering a sustainable future for generations to come
        </ServicePreview>
        <ServicePreview class="max-w-xl bg-zinc-900 p-8" icon="ph:chalkboard-teacher-light" title="Philanthrophy">
          Using technology to drive philanthropic initiatives, aiming to enhance social welfare and foster equitable access to resources through innovative solutions and community empowerment.
        </ServicePreview>
      </div>
      <div class="flex justify-center">
        <ServicePreview class="max-w-xl bg-zinc-900 p-8" icon="mdi:help-circle-outline" title="Research">
          Researching to advance knowledge and innovate solutions for complex societal challenges is my career objective. To know the unknown
        </ServicePreview>
      </div>
    </AppSection>
  </div>
</template>