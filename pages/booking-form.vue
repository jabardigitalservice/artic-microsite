<template>
  <div class="p-8">
    <div class="rounded-lg border border-blue-500">
      <div class="px-4 py-5 sm:p-6">
        <h3 class="leading-6 font-bold text-gray-900">Data Calon Pengunjung</h3>
        <div class="mt-2 max-w-xl text-sm leading-5 text-gray-900">
          <p>
            Silahkan isi kelengkapan informasi calon pengunjung Jabar Command
            Center.
          </p>
        </div>
      </div>
    </div>
    <div class="mt-8">
      <div>
        <label
          for="name"
          class="block text-gray-700 leading-5 text-sm font-medium"
        >
          Nama Penanggung Jawab
          <span class="text-red-500">*</span>
        </label>
        <div class="mt-1 relative rounded-md">
          <input
            id="name"
            v-model="name"
            type="text"
            name="name"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          />
        </div>
      </div>
      <div class="mt-4">
        <div>
          <label
            for="personal_identity"
            class="block text-gray-700 leading-5 text-sm font-medium"
          >
            Nomor Identitas Penanggung Jawab (NIK)
            <span class="text-red-500">*</span>
          </label>
          <div class="mt-1 relative rounded-md">
            <input
              id="personal_identity"
              v-model="personal_identity"
              type="text"
              name="name"
              class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
            />
          </div>
        </div>
      </div>
      <div class="mt-4">
        <label
          for="organization_name"
          class="block text-gray-700 leading-5 text-sm font-medium"
        >
          Nama Organisasi / Instansi
          <span class="text-red-500">*</span>
        </label>
        <div class="mt-1 relative rounded-md">
          <input
            id="organization_name"
            v-model="organization_name"
            type="text"
            name="organization_name"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          />
        </div>
      </div>
      <div class="mt-4">
        <label
          for="address"
          class="block text-gray-700 leading-5 text-sm font-medium"
        >
          Alamat Penanggung Jawab / Organisasi / Instansi
          <span class="text-red-500">*</span>
        </label>
        <div class="mt-1 relative rounded-md">
          <input
            id="address"
            v-model="address"
            type="text"
            name="address"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          />
        </div>
      </div>
      <div class="mt-4">
        <label
          for="phone_number"
          class="block text-gray-700 leading-5 text-sm font-medium"
        >
          Nomor Telepon
          <span class="text-red-500">*</span>
        </label>
        <div class="mt-1 relative rounded-md">
          <input
            id="phone_number"
            v-model="phone_number"
            type="text"
            name="phone_number"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          />
        </div>
      </div>
      <div class="mt-4">
        <label
          for="peoples_count"
          class="block text-gray-700 leading-5 text-sm font-medium"
        >
          Estimasi Jumlah Peserta
          <span class="text-red-500">*</span>
        </label>
        <div class="mt-1 relative rounded-md">
          <input
            id="peoples_count"
            v-model="peoples_count"
            type="number"
            name="peoples_count"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          />
        </div>
      </div>
      <div class="mt-4">
        <label
          for="schedule_id"
          class="block text-gray-700 leading-5 text-sm font-medium"
        >
          Jadwal Kunjungan
          <span class="text-red-500">*</span>
        </label>
        <div class="mt-1 relative rounded-md">
          <input
            id="schedule_id"
            v-model="schedule_id"
            type="text"
            name="schedule_id"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          />
        </div>
      </div>
      <div class="mt-8 text-center">
        <button
          type="submit"
          class="block w-full bg-blue-500 text-white font-semibold text-center py-2 px-4 rounded"
          @click="submit"
        >
          Simpan
        </button>
        <nuxt-link
          to="/booking"
          class="block w-full text-blue-700 font-semibold text-center py-2 px-4 border border-blue-500 rounded mt-2"
        >
          Kembali
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2'

export default {
  data() {
    return {
      name: null,
      personal_identity: null,
      organization_name: null,
      address: null,
      phone_number: null,
      peoples_count: null,
      schedule_id: null,
    }
  },

  methods: {
    async submit() {
      try {
        await this.$axios.post(`/register`, {
          name: this.name,
          personal_identity: this.personal_identity,
          organization_name: this.organization_name,
          address: this.address,
          phone_number: this.phone_number,
          peoples_count: this.peoples_count,
          schedule_id: this.schedule_id,
        })

        await Swal.fire(
          '',
          'Permintaan reservasi berhasil dibuat. Silahkan unduh bukti pendaftaran.',
          'success'
        )
      } catch (e) {
        //
      }
    },
  },
}
</script>
