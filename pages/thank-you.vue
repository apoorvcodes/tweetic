<script setup lang="ts">
const tweets = ref([
  "https://twitter.com/dominiksumer/status/1524741858009694209",
  "https://twitter.com/maazarin/status/1524732072832774147",
  "https://twitter.com/kecrily/status/1524665293540589569",
  "https://twitter.com/pramit_armpit/status/1524637652565524481",
  "https://twitter.com/ImnNazri/status/1524626328167010304",
  "https://twitter.com/frouo/status/1524840028123320326",
])

useCustomHead("Thank you for your kind word! | Tweetic")
</script>

<template>
  <div class="mb-32">
    <h2 class="text-4xl md:text-6xl text-center font-semibold my-8 md:my-20">Thank you everyone!!</h2>

    <Masonry :urls="tweets" :column-width="400" :options="{ layout: 'supabase' }">
      <template v-slot="{ url, options }">
        <Tweet class="flex justify-center" :url="url" v-bind="options"></Tweet>
      </template>
    </Masonry>

    <p class="text-center mt-8 md:mt-20">...and everyone who likes and retweet!</p>
  </div>
</template>
