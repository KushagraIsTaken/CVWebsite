<script setup lang="ts">
definePageMeta({
  documentDriven: false
})

const title = 'Resume - Kushagra Agrawal'
const description = 'View or download the resume of Kushagra Agrawal.'

useSeoMeta({
  title,
  description,
})

defineOgImageComponent('General')

// Redirect to Google Drive link
onMounted(() => {
  window.location.href = 'https://drive.google.com/file/d/15Dgz1RFnetcWqhykw-TP_1vlbX_2dCd6';
});
</script>

<template>
  <div>
    <AppSection>
      <ParagraphDecoration />
      <AppParagraph look="heading" class="mt-4" tag="h1">Redirecting to my Resume...</AppParagraph>
      <p>If you are not redirected automatically, <a href="https://drive.google.com/file/d/15Dgz1RFnetcWqhykw-TP_1vlbX_2dCd6">click here</a>.</p>
    </AppSection>
  </div>
</template>

<style scoped>
/* Add any styles you need here */
</style>
