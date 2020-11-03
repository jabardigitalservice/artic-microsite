<template>
  <div>
    <div id="logo">
      <Logo />
    </div>
    <div class="p-8">
      <nuxt-link
        to="/booking"
        class="block w-full bg-blue-500 text-white font-semibold text-center py-2 px-4 rounded"
      >
        Reservasi Kunjungan
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    // Ping Backend Service
    this.$axios.$get(`/`)
  },
}
</script>
