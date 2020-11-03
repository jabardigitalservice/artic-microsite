<template>
  <div class="p-8">
    <h3 class="text-center leading-6 font-bold text-gray-900">
      Selamat Datang
    </h3>
    <div class="mt-4 text-sm">
      <p>
        Jabar Command Center merupakan fasilitas publik yang dikelola oleh
        Pemerintah Provinsi Jawa Barat.
      </p>
      <p class="mt-4">
        Saat ini Jabar Command Center menerapkan pembatasan berupa kuota
        kunjungan sebagai bagian dari penerapan protokol kesehatan.
      </p>
      <p class="mt-4">
        Silakan lakukan reservasi kunjungan dengan selalu menggunakan masker dan
        tetap patuhi protokol kesehatan yang ada.
      </p>
    </div>

    <div class="mt-12 text-center">
      <nuxt-link
        to="/booking-form"
        class="block w-full bg-blue-500 text-white font-semibold text-center py-2 px-4 rounded"
      >
        Ya, Saya Mengerti
      </nuxt-link>
      <nuxt-link
        to="/"
        class="block w-full text-blue-700 font-semibold text-center py-2 px-4 border border-blue-500 rounded mt-2"
      >
        Kembali
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  //
}
</script>
