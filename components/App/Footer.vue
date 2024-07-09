<script setup lang="ts">
const navigation = {
  content: [
    { name: 'Publications', to: '/articles/' },
    { name: 'Events', to: '/speaking/' },
    { name: 'Resume', to: "https://drive.google.com/file/d/1QEgKlGB0nvWx3KZVkkibFPhVRcQiz-2m" },
    { name: 'Curriculum Vitae', to: "https://drive.google.com/file/d/1yXRK-dRtuV2UKoHfMlPycxIwQHiJ-fCQ" },
  ],
  general: [
    { name: 'About', to: '/about/' },
    // { name: 'My equipment', to: '/uses/' },

  ],
  services: [
    { name: 'Google Scholar', to: "https://scholar.google.com/citations?user=hZgi4BgAAAAJ&hl=en" },
    { name: 'ORCiD', to: "https://orcid.org/0009-0006-7753-175X" }, 
    { name : 'ResearchGate', to: "https://www.researchgate.net/profile/Kushagra-Agrawal-20"},
    // { name: 'Testimonials', to: '/testimonials/' },
  ],
  contact: [
    { name: 'Contact me', to: '/contact/' },
    { name: 'Schedule Meeting', to: "https://topmate.io/kushagra_agrawal"}
  ],
  social: [
    {
      name: 'GitHub',
      href: "https://github.com/KushagraIsTaken",
      icon: 'mdi:github',
      hoverClass: 'hover:text-gray-200'
    },
    {
      name: 'LinkedIn',
      href: "https://www.linkedin.com/in/kushagra-agrawal-51a3121ab/",
      icon: 'mdi:linkedin',
      hoverClass: 'hover:text-blue-500'
    },
    {
      name: 'Instagram',
      href: "https://www.instagram.com/kushagra_0017_official/",
      icon: 'mdi:instagram',
      hoverClass: 'hover:text-blue-500'
    },
    {
      name: 'Medium',
      href: "https://medium.com/@kush4409",
      icon: 'mdi:medium',
      hoverClass: 'hover:text-blue-500'
    },
  ],
}

type NewsletterState = 'initial' | 'loading' | 'error' | 'confirmation-mail-sent'
const state = ref<NewsletterState>('initial')
const form = ref({
  name: '',
  email: ''
})

const { addNotification } = useNotifications() 

async function subscribeToNewsletter() {
  if(state.value === 'loading') {
    return
  }
  
  state.value = 'loading'
  const { name, email } = form.value
  try {
    await $fetch('/api/newsletter/subscribe/', {
      method: 'POST',
      body: { name, email }
    })
    state.value = 'confirmation-mail-sent'
    addNotification({
      heading: 'Almost done!',
      body: 'Thanks for subscribing to my newsletter! 🎉 Please confirm your email now!',
      iconName: 'heroicons:check-badge',
      iconClass: 'text-green-500',
      durationInMs: 10000,
    })
    form.value = { name: '', email: '' }
  } catch (error) {
    // TODO: Better error handling
    // @ts-expect-error Better type checking needed but too lazy on stream. Sorry
    const body = error?.data?.message ?? error.message
    addNotification({
      heading: 'Something went wrong!',
      body,
      iconName: 'heroicons:exclamation-circle',
      iconClass: 'text-red-500',
      durationInMs: 10000,
    })
    console.error(error)
    state.value = 'error'
  }
}
</script>
<template>
  <footer class="bg-zinc-900" aria-labelledby="footer-heading">
    <h2 id="footer-heading" class="sr-only">Footer</h2>
    <div class="mx-auto max-w-7xl px-6 pb-8 pt-8 sm:pt-16 lg:px-8 xl:pt-32">
      <div class="xl:grid xl:grid-cols-4 xl:gap-8">
        <NuxtPicture format="avif,webp,png" width="256" height="200" densities="x1 x2" placeholder :img-attrs="{ class: 'z-20 relative' }"
          src="img/footer_logo.png" alt="Photo of Kushagra Agrawal" />
        <div class="grid grid-cols-2 gap-8 xl:col-span-3 pt-16 xl:pt-0">
          <div class="md:grid md:grid-cols-2 md:gap-8">
            <div>
              <h3 class="text-sm font-semibold leading-6 text-white">Content</h3>
              <ul role="list" class="mt-6 space-y-4">
                <li v-for="item in navigation.content" :key="item.name">
                  <AppLink :to="item.to" class="text-sm leading-6 text-gray-300 hover:text-white">{{ item.name }}
                  </AppLink>
                </li>
              </ul>
            </div>
            <div>
              <h3 class="text-sm font-semibold leading-6 text-white">Research Profiles</h3>
              <ul role="list" class="mt-6 space-y-4">
                <li v-for="item in navigation.services" :key="item.name">
                  <AppLink :href="item.to" class="text-sm leading-6 text-gray-300 hover:text-white">{{ item.name }}
                  </AppLink>
                </li>
              </ul>
            </div>
            
          </div>
          <div class="md:grid md:grid-cols-2 md:gap-8">

            <div class="mt-10 md:mt-0">
              <h3 class="text-sm font-semibold leading-6 text-white">Contact</h3>
              <ul role="list" class="mt-6 space-y-4">
                <li v-for="item in navigation.contact" :key="item.name">
                  <AppLink :to="item.to" class="text-sm leading-6 text-gray-300 hover:text-white">{{ item.name }}
                  </AppLink>
                </li>

              </ul>
            </div>
            <div class="mt-10 md:mt-0">
              <h3 class="text-sm font-semibold leading-6 text-white">General</h3>
              <ul role="list" class="mt-6 space-y-4">
                <li v-for="item in navigation.general" :key="item.name">
                  <AppLink :href="item.to" class="text-sm leading-6 text-gray-300 hover:text-white">{{ item.name }}
                  </AppLink>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    <div class="mt-8 border-t border-white/10 pt-8 md:flex md:items-center md:justify-between">
        <div class="flex space-x-6 md:order-2">
          <a target="_blank" v-for="item in navigation.social" :key="item.name" :href="item.href" class="text-gray-400"
            :class="item.hoverClass">
            <span class="sr-only">{{ item.name }}</span>
            <Icon :name="item.icon" class="h-6 w-6" aria-hidden="true" />
          </a>
        </div>

      </div>
    </div>
  </footer>
</template>