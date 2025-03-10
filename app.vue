<script setup lang="ts">
import { provideUseId } from '@headlessui/vue'
provideUseId(() => useId())

const route = useRoute()

useAppSeo()
useSiteNotifications()

function useAppSeo() {
  const isDark = useDark()
  const favicon = computed(() => `/img/logo/glyph-${isDark.value ? 'white' : 'black'}-colored.svg`)

  useServerHead({
    bodyAttrs: {
      class: 'bg-black antialiased min-h-screen text-white'
    },
  })

  useHead({
    titleTemplate: (c) => c ? `${c} - Kushagra Agrawal` : 'Kushagra Agrawal - AI Engineer',
    link: [
      { rel: 'icon', href: favicon, type: "image/svg+xml" },
    ],
  })

  useSchemaOrg([
    definePerson({
      address: {
        '@type': 'PostalAddress',
        addressCountry: 'IN',
        addressLocality: 'Hyderabad',
        addressRegion: 'Shivarampally',
        postalCode: '500030',
        streetAddress: '305, Tower 12, Provident Kenworth'
      },
      name: 'Kushagra Agrawal',
      image: '/img/kush-pp.png',
      email: 'mailto:kush4409@gmail.com',
      nationality: "Indian",
      jobTitle: 'Research Intern',
      url: 'https://www.kushagraagrawal.online/',
      sameAs: [
        ...Object.values(SOCIALS),
        'https://stackoverflow.com/',
        'https://www.developmint.de/',
      ]
    }),
    defineWebSite(),
    defineWebPage()
  ])

  useServerSeoMeta({
    author: 'Kushagra Agrawal',
    ogSiteName: 'www.kushagraagrawal.online',
  })

  const styleConfig = {
    hideEventTypeDetails: false,
    layout: "month_view"
  }

  // Cal.com
  // TODO: Defer loading later on but store clicks in the meantime
  useHead({
    script: [
      {
        key: 'cal',
        innerHTML: `
(function (C, A, L) { let p = function (a, ar) { a.q.push(ar); }; let d = C.document; C.Cal = C.Cal || function () { let cal = C.Cal; let ar = arguments; if (!cal.loaded) { cal.ns = {}; cal.q = cal.q || []; d.head.appendChild(d.createElement("script")).src = A; cal.loaded = true; } if (ar[0] === L) { const api = function () { p(api, arguments); }; const namespace = ar[1]; api.q = api.q || []; typeof namespace === "string" ? (cal.ns[namespace] = api) && p(api, ar) : p(cal, ar); return; } p(cal, ar); }; })(window, "https://app.cal.com/embed/embed.js", "init");
Cal("init", {origin:"https://cal.com"});
Cal("ui", ${JSON.stringify(styleConfig)});
`,
      }
    ]
  })
}

function useSiteNotifications() {
  const { addNotification } = useNotifications()

  onMounted(async () => {
    const result = onDicsordRef()
    if (result) {
      await new Promise((resolve) => setTimeout(resolve, 1000))
    }
  })

  function onDicsordRef(): Boolean {
    const isDicsordDomain = route.query?.ref === 'dicsord.com'
    if (!isDicsordDomain) {
      return false
    }

    addNotification({
      heading: 'You should double check the URL 😛',
      body: [
        { type: 'text', text: 'Did you want to go to ' },
        { type: 'link', href: 'https://discord.com/' },
        { type: 'text', text: ' instead?' },
      ]
    })
    return true
  }
}
</script>

<template>
  <div>
    <AppNavbar />
    <div class="mt-8">
      <NuxtPage />
    </div>
    <!-- Gradient "hack" for icons -->
    <svg style="width:0;height:0;position:absolute;" aria-hidden="true" focusable="false">
      <linearGradient id="gradient-svg-icon" x2="1" y2="1">
        <stop offset="0" style="stop-color:#F20500" />
        <stop offset="2.272730e-04" style="stop-color:#F20500" />
        <stop offset="1" style="stop-color:#D90575" />
      </linearGradient>
    </svg>
    <LazyAppFooter />
    <LazyAppNotificationArea />
  </div>
</template>

<style lang="pcss">
::selection {
  @apply bg-red-500/25;
}

/* TODO: Move to ProseCode component? */
.line {
  display: inline-table;
  @apply -mx-8 px-8;
}

.line.highlight {
  @apply bg-white/5;
}
</style>
