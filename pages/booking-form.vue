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
              v-model="personalIdentity"
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
            v-model="organizationName"
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
            v-model="phoneNumber"
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
            v-model="peoplesCount"
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
          <select
            id="schedule_id"
            v-model="scheduleId"
            type="text"
            name="schedule_id"
            class="block pr-10 border-2 rounded w-full py-2 px-2 text-gray-700 leading-tight focus:outline-none"
          >
            <option
              v-for="schedulesOption in schedulesOptions"
              :key="schedulesOption['id']"
              :value="schedulesOption['value']"
            >
              {{ schedulesOption['text'] }}
            </option>
          </select>
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
import { format } from 'date-fns'
import { id } from 'date-fns/locale'

export default {
  data() {
    return {
      name: null,
      personalIdentity: null,
      organizationName: null,
      address: null,
      phoneNumber: null,
      peoplesCount: null,
      scheduleId: null,
      schedulesOptions: [],
    }
  },

  mounted() {
    this.fetchSchedules()
  },

  methods: {
    async fetchSchedules() {
      try {
        const { data: schedules } = await this.$axios.$get(
          `/register/schedules`
        )

        this.schedulesOptions = schedules.map((schedule) => {
          const dateStart = new Date(schedule.start_at)
          const dateText = format(dateStart, 'eeee, dd MMMM yyyy HH:mm', {
            locale: id,
          })

          return {
            value: schedule.id,
            text: `${dateText} (Kapasitas Tersedia: ${schedule.quota_available} orang)`,
          }
        })
      } catch (error) {
        //
      }
    },

    async submit() {
      try {
        await this.$axios.$post(`/register`, {
          name: this.name,
          personal_identity: this.personalIdentity,
          organization_name: this.organizationName,
          address: this.address,
          phone_number: this.phoneNumber,
          peoples_count: this.peoplesCount,
          schedule_id: this.scheduleId,
        })

        await Swal.fire(
          '',
          'Permintaan reservasi berhasil dibuat. Silahkan unduh bukti pendaftaran.',
          'success'
        )
      } catch (error) {
        if (error.response && error.response.status === 422) {
          const firstErrorKey = Object.keys(error.response.data.errors)[0]
          const firstMessage = error.response.data.errors[firstErrorKey][0]

          return await Swal.fire('', firstMessage, 'error')
        }

        return await Swal.fire(
          'Telah terjadi kesalahan sistem',
          'Silahkan ulangi beberapa saat kembali.',
          'error'
        )
      }
    },
  },
}
</script>
