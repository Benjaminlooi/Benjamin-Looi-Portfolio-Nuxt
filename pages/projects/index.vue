<template>
  <div ref="root" class="container mx-auto">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4">
      <div
        v-for="(project, i) in projectsData"
        :key="i"
        class="px-4 py-8 max-w-xl"
      >
        <div class="bg-white shadow-2xl h-full">
          <a :href="project.projectLink">
            <nuxt-img
              :src="`/img/${project.imageSrc}`"
              :alt="project.imageAlt"
            />
          </a>

          <div class="p-4 bg-white">
            <h2 class="font-bold text-2xl text-gray-800 flex items-center">
              {{ project.projectTitle }}
              <a
                :href="project.projectLink"
                class="text-base text-blue-400 hover:text-blue-500 ml-1.5"
                ><font-awesome-icon icon="external-link-alt"
              /></a>
            </h2>
            <p class="sm:text-sm text-xs text-gray-700 mt-1">
              <span v-html="project.projectDesc"></span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import projectsData from './projects_data'

export default {
  data: () => ({
    projectsData,
  }),
  head() {
    return {
      title: 'BENJAMIN LOOI | WEB DEVELOPER | PROJECTS',
    }
  },
  mounted() {
    if (process.browser) {
      const ImagesLoaded = require('imagesloaded')

      const rootRef = this.$refs.root

      ImagesLoaded(rootRef, () => {
        this.$nuxt.$emit('update-locomotive')
      })
    }
  },
}
</script>

<style></style>
