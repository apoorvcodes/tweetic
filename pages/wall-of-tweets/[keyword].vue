<script setup lang="ts">
import { capitalizeFirstLetter } from "~~/utils/function"
const route = useRoute()
const keyword = route.params.keyword?.toString()

const { data, pending } = await useAsyncData(keyword, () =>
  $fetch("/api/wall-of-tweets", {
    params: { keyword },
  })
)

useCustomHead(`${capitalizeFirstLetter(keyword.toString())}'s Wall of Tweets! | Tweetic`)
</script>

<template>
  <div>
    <div class="flex flex-col items-center justify-center my-8 md:my-16 md:space-y-2">
      <h2 class="font-bold text-4xl md:text-6xl capitalize">{{ keyword }}'s</h2>
      <h3 class="font-semibold text-2xl md:text-4xl text-gray-300">Wall of Tweets</h3>
    </div>

    <template v-if="data.length">
      <Masonry :urls="data" :column-width="400" :options="{ layout: 'supabase', show_media: true, show_info: true }">
        <template v-slot="{ url, options }">
          <Tweet class="flex justify-center" :url="url" v-bind="options"></Tweet>
        </template>
      </Masonry>
    </template>
    <p v-else class="text-center my-40 text-gray-300 font-semibold">No tweets crawled...</p>
  </div>
</template>
