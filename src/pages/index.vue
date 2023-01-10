<template>
  <SenpLayoutBasic
    fixed-header
    :classes="{
      header: {
        extend: 'text-base sm:text-xl md:text-2xl bg-black/40 backdrop-blur border-b border-neutral-800/60 shadow',
      },
    }"
  >
    <template #header>
      <div class="flex items-center gap-1.5 sm:gap-3">
        <img src="@/assets/logo.svg" class="w-8 h-8" alt="" />
        <p class="tracking-wide">Fleur.codes</p>
      </div>

      <div class="flex items-center gap-1.5 sm:gap-3">
        <a
          href="https://github.com/nicolehollant/portfolio"
          target="_blank"
          rel="noopener noreferrer"
          class="h-max items-center text-neutral-200 hover:text-blue-400 transition"
          ><Icon name="mdi:github"></Icon
        ></a>
      </div>
    </template>

    <template #content>
      <section
        class="flex flex-col lg:flex-row items-center justify-start gap-4 lg:gap-8 pt-4 pb-16 lg:pb-4 lg:h-[90vh]"
        v-for="app in state.mainApps"
      >
        <div class="grid gap-1 w-full lg:w-2/3">
          <div class="text-xs uppercase font-semibold tracking-wider text-neutral-500 line-clamp-1">
            {{ app.name }} gallery
          </div>
          <Carousel
            :images="app.images"
            mode="manual"
            class="rounded-lg overflow-hidden border-2 border-neutral-800"
          ></Carousel>
        </div>
        <div class="w-full flex flex-col gap-2 lg:w-1/3">
          <h3 class="text-2xl">{{ app.name }}</h3>
          <p class="text-neutral-400">{{ app.description }}</p>
          <a :href="app.link" target="_blank" rel="noopener noreferrer" class="mt-2 w-max">
            <SenpButton class="!px-6">Visit <Icon name="mdi:arrow-right" /></SenpButton>
          </a>
        </div>
      </section>
      <h2 class="text-2xl py-6">Smaller Projects</h2>
      <div class="grid gap-6 sm:gap-8 lg:gap-12 grid-cols-2">
        <section
          class="flex flex-col lg:flex-row items-center justify-start gap-4 lg:gap-8 py-4"
          v-for="app in state.secondaryApps"
        >
          <div class="grid gap-1 w-full lg:w-3/5" v-if="app.image">
            <div class="text-[10px] uppercase font-semibold tracking-wider text-neutral-500 line-clamp-1">
              {{ app.name }} gallery
            </div>
            <Carousel
              :images="[app.image]"
              mode="manual"
              class="rounded-lg overflow-hidden border-2 border-neutral-800"
            ></Carousel>
          </div>
          <div class="w-full flex flex-col gap-2 lg:w-2/5">
            <a :href="app.link" target="_blank" rel="noopener noreferrer" class="flex items-center gap-2 group">
              <h3 class="text-lg sm:text-2xl group-hover:underline">{{ app.name }}</h3>
              <Icon class="text-lg text-neutral-400 group-hover:text-blue-400" name="mdi:link-variant" />
            </a>
            <p class="text-sm sm:text-base text-neutral-400">{{ app.description }}</p>
          </div>
        </section>
      </div>
      <div class="h-40"></div>
    </template>
    <template #footer>
      <p class="text-center text-neutral-400">made with 💚 by nicole</p>
    </template>
  </SenpLayoutBasic>
</template>

<script setup lang="ts">
const state = reactive<{
  mainApps: { name: string; description: string; link: string; images: { src: string; alt: string }[] }[]
  secondaryApps: { name: string; description: string; link: string; image?: { src: string; alt: string } }[]
}>({
  mainApps: [
    {
      name: 'Crudify',
      description:
        "Crudify is a free (until it's unsupportable) SaaS product for rapidly creating REST APIs for a generated schema as well as providing magic link based user pools for authentication",
      link: 'https://crudify.app',
      images: [
        { src: '/example-images/crudify/01_home.png', alt: 'Screenshot of Crudify home page' },
        { src: '/example-images/crudify/02_dashboard.png', alt: 'Screenshot of Crudify dashboard page' },
        { src: '/example-images/crudify/03_create.png', alt: 'Screenshot of Crudify create page' },
        { src: '/example-images/crudify/04_enitity.png', alt: 'Screenshot of Crudify entity page' },
        { src: '/example-images/crudify/05_create-entity.png', alt: 'Screenshot of Crudify create entity page' },
        { src: '/example-images/crudify/06_explore-entity.png', alt: 'Screenshot of Crudify explore entity page' },
      ],
    },
    {
      name: 'Dataviewer',
      description:
        'Dataviewer is a general-purpose spreadsheet viewer able to be configured to beautifully render any spreadsheet in browser. Powered by SenpUI',
      link: 'https://dataviewer.crudify.app',
      images: [
        { src: '/example-images/dataviewer/01_home.png', alt: 'Screenshot of Dataviewer home page' },
        { src: '/example-images/dataviewer/02_sheets.png', alt: 'Screenshot of Dataviewer sheets page' },
        { src: '/example-images/dataviewer/03_base-data.png', alt: 'Screenshot of Dataviewer base data view' },
        { src: '/example-images/dataviewer/04_settings.png', alt: 'Screenshot of Dataviewer settings view' },
        { src: '/example-images/dataviewer/05_modified.png', alt: 'Screenshot of Dataviewer modified data view' },
      ],
    },
    {
      name: 'FakerUI',
      description:
        'FakerUI is a UI around fakerjs used for quickly generating fake data that conforms to a schema. Powered by SenpUI',
      link: 'https://faker-ui.crudify.app',
      images: [
        { src: 'example-images/faker-ui/01_home.png', alt: 'Screenshot of FakerUI home' },
        { src: 'example-images/faker-ui/02_shared-models.png', alt: 'Screenshot of FakerUI shared models modal' },
        { src: 'example-images/faker-ui/03_model.png', alt: 'Screenshot of FakerUI model' },
        { src: 'example-images/faker-ui/04_faker-modal.png', alt: 'Screenshot of FakerUI faker value modal' },
      ],
    },
    {
      name: 'Spotify Brackets',
      description:
        'Spotify Brackets is an app that connects to the Spotify API and allows users to create a single-elimination bracket from a playlist (may be down if inactive)',
      link: 'https://spotify-brackets.fleur.codes/',
      images: [
        { src: 'example-images/spotify-brackets/01_home.png', alt: 'Screenshot of Spotify Brackets home' },
        { src: 'example-images/spotify-brackets/02_bracket.png', alt: 'Screenshot of Spotify Brackets bracket' },
        { src: 'example-images/spotify-brackets/02_results.png', alt: 'Screenshot of Spotify Brackets results' },
        {
          src: 'example-images/spotify-brackets/02_results-bracket.png',
          alt: 'Screenshot of Spotify Brackets results bracket',
        },
      ],
    },
  ],
  secondaryApps: [
    {
      name: 'Devtools',
      description: 'Devtools is a small app for converting between JSON and YAML or between JSON and CSV',
      link: 'https://devtools.fleur.codes/yaml',
      image: { src: '/example-images/misc/devtools.png', alt: 'Screenshot of Devtools' },
    },
    {
      name: 'SenpUI',
      description:
        'Senp-ui is a simple component library for nuxt3 with the intention of being used via nuxt extends (it powers this site!)',
      link: 'https://chipper-elf-034ac0.netlify.app/',
      image: { src: '/example-images/misc/senp-ui.png', alt: 'Screenshot of SenpUI' },
    },
    {
      name: 'Twittify',
      description: 'Twittify is a small Twitter clone made with Crudify',
      link: 'https://twittify.crudify.app/',
      image: { src: '/example-images/misc/twittify.png', alt: 'Screenshot of Twittify' },
    },
    {
      name: 'Fleurdle',
      description: 'Fleurdle is a wordle clone with the option to use N-letter words and the option to create puzzles',
      link: 'https://fleurdle.fleur.codes/',
      image: { src: '/example-images/misc/fleurdle.png', alt: 'Screenshot of Fleurdle' },
    },
    {
      name: 'T3dium',
      description: 'T3dium is a quick dynamic blog made to test out the T3 stack (currently down)',
      link: 'https://t3dium.fleur.codes/',
      image: { src: '/example-images/misc/t3dium.png', alt: 'Screenshot of T3dium' },
    },
    {
      name: 'Curvy Spline Editor',
      description: "Curvy Spline Editor is a UI for editing splines from Tim's curvy package",
      link: 'https://super-tapioca-04789b.netlify.app/',
      image: { src: '/example-images/misc/curvy-editor.png', alt: 'Screenshot of Curvy Editor' },
    },
    {
      name: 'Noise',
      description:
        'Noise is an old school project with perlin-noise based animated backgrounds and a player for 3 auto-generated midi tracks',
      link: 'https://thriving-meerkat-7d158b.netlify.app/',
      image: { src: '/example-images/misc/noise.png', alt: 'Screenshot of Noise' },
    },
    {
      name: 'FFMpeg Utils',
      description: 'FFMpeg Utils is a video and image format converter using the ffmpeg wasm module',
      link: 'https://ffmpeg.fleur.codes/',
      image: { src: '/example-images/misc/ffmpeg.png', alt: 'Screenshot of FFMpeg Utils' },
    },
    {
      name: 'UI Pad',
      description:
        'UI Pad is a UI playground that supports rendering many views at different sizes with TailwindCSS as a CSS framework (from before they made tailwind play!)',
      link: 'https://ui-pad.vercel.app/playground',
      image: { src: '/example-images/misc/ui-pad-1.png', alt: 'Screenshot of UI Pad' },
    },
    {
      name: 'Math Pad',
      description: 'Math Pad is a Math playground that supports basic TeX and markdown',
      link: 'https://math-pad.vercel.app/#/',
      image: { src: '/example-images/misc/math-pad.png', alt: 'Screenshot of Math Pad' },
    },
    {
      name: 'UI Pad v2',
      description:
        'UI Pad v2 is a work in progress (well... was a work in progress) iteration on UI Pad succeeded by the SenpUI playground',
      link: 'https://ui-pad.fleur.codes/editor',
      image: { src: '/example-images/misc/ui-pad-2.png', alt: 'Screenshot of UI Pad v2' },
    },
    {
      name: 'Minecraft Test',
      description: 'Minecraft Test was a way for me to try out some 3D rendering / physics in JS',
      link: 'https://lucid-brown-e927f5.netlify.app/',
      image: { src: '/example-images/misc/minecraft.png', alt: 'Screenshot of Minecraft' },
    },
    {
      name: 'Tweet Replacer',
      description:
        'Tweet Replacer was a small project for a friend who wanted to obfuscate her twitter posts by replacing all characters as asterisks or base64 encoding the tweet content',
      link: 'https://mystifying-galileo-471507.netlify.app/',
      image: { src: '/example-images/misc/tweet-replacer.png', alt: 'Screenshot of Tweet replacer' },
    },
  ],
})
</script>
