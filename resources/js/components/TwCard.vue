<template>
  <div class="card p-8 bg-white mb-6 rounded-lg shadow-lg">
    <img v-if="image" class="w-full" :src="image" :alt="imageAlt" :title="imageAlt">
    <div v-if="title" class="card-header font-bold text-xl mb-2">
      {{ title }}
    </div>
    <div class="card-body">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'TwCard',

  props: {
    title: { type: String, default: null },
    image: { type: String, default: null },
    imageAlt: { type: String, default: null },
  }
}
</script>
