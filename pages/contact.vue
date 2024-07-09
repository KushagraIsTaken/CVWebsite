<script setup lang="ts">
definePageMeta({
  documentDriven: false
})

const title = 'Contact me - Kushagra Agrawal'
const description = 'Reach out for a project or consulting inquiry, to give feedback or just to say hi. Easiest via email or one of the social media platforms below'

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
      <AppParagraph look="heading" class="mt-4" tag="h1">Contact</AppParagraph>
      <AppParagraph class="mt-16 text-lg max-w-prose">
        <b>Hey there!</b> I'm always happy to hear from you. If you have any questions, or feedback or just want to say
        hi, feel free to reach out to me on any of the platforms linked in the footer or via email at <a href="mailto:kush4409@gmail.com">kush4409@gmail.com</a>, <a href="mailto:2205044@kiit.ac.in">2205044@kiit.ac.in</a>, or <a href="mailto:kushagra.agrawal@ieee.org">kushagra.agrawal@ieee.org</a>.
      </AppParagraph>
      <AppParagraph class="mt-12 text-lg max-w-prose">
        You can also <AppMeetingButtonWrapper meeting="intro-website"><button
            class="underline hover:no-underline">schedule a meeting with me</button></AppMeetingButtonWrapper> easily!
      </AppParagraph>
      <AppParagraph class="mt-12 text-lg max-w-prose">
        I usually respond within 12 to 24 hours.
      </AppParagraph>
    </AppSection>
  </div>
</template>