<template>
  <div v-if="showModal">
    <Modal v-if="showModal" @close="toggleModal" :delay="delay">
      <template v-slot:details>
        <div v-if="isSuccess">
          <h1>Success!</h1>
          <p>Your data has been sent to system ^_^</p>
          <a href="#" @click="toggleModal">Close</a>
        </div>
        <div v-else>
          <h1 style="color: red">Failed!</h1>
          <p>Your data hasn't been sent to system T_T</p>
          <a href="#" @click="toggleModal">Close</a>
        </div>
      </template>
    </Modal>
  </div>
  <form @submit.prevent="handleSubmit">
    <h2>Registrasi Penerima Bantuan Sosial</h2>
    <label>Nama:</label>
    <input type="text" required v-model="nama">

    <!-- <label>NIK:</label>
    <input type="number" required v-model="nik">

    <label>Nomor Kartu Keluarga:</label>
    <input type="number" required v-model="noKk">

    <label>Foto KTP:</label>
    <input type="file" required>

    <label>Foto Kartu Keluarga:</label>
    <input type="file" required>

    <label>Umur:</label>
    <input type="number" required v-model="umur"> -->

    <label>Jenis Kelamin:</label>
    <select v-model="jenisKelamin">
      <!-- <option v-for="item in JenisKelaminEnum" :key="item">{{ item }}</option> -->
      <option value="0">Laki-laki</option>
      <option value="1">Perempuan</option>
    </select>

    <!-- <label>Provinsi:</label>
    <select v-model="provinsi">
      <option value="0">Jakarta Selatan</option>
      <option value="1">Jakarta Barat</option>
    </select>

    <label>Kab/Kota:</label>
    <select v-model="kabupaten">
      <option value="0">Jakarta Selatan</option>
      <option value="1">Jakarta Barat</option>
    </select>

    <label>Kecamatan:</label>
    <select v-model="kecamatan">
      <option value="0">Jakarta Selatan</option>
      <option value="1">Jakarta Barat</option>
    </select>

    <label>Kelurahan/Desa:</label>
    <select v-model="kelurahan">
      <option value="0">Jakarta Selatan</option>
      <option value="1">Jakarta Barat</option>
    </select>

    <label>Alamat:</label>
    <textarea required v-model="alamat"></textarea>

    <label>RT:</label>
    <input type="number" required v-model="rt">

    <label>RW:</label>
    <input type="number" required v-model="rw">

    <label>Penghasilan sebelum pandemi:</label>
    <input type="number" required v-model="penghasilanSebelumPandemi">

    <label>Penghasilan setelah pandemi:</label>
    <input type="number" required v-model="penghasilanSetelahPandemi">

    <label>Alasan membutuhkan bantuan:</label>
    <input type="text" required v-model="alasan"> -->

    <div class="container">
      <input type="checkbox" v-model="terms" required>
      <label>Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.</label>
    </div>

    <div class="submit">
      <button :disabled="showModal" >Register</button>
    </div>
  </form>
</template>

<script>
import Modal from './Modal.vue'

export default {
  data() {
    return {
      nama: '',
      nik: '',
      noKk: '',
      umur: '',
      jenisKelamin: '',
      provinsi: '',
      kabupaten: '',
      kecamatan: '',
      kelurahan: '',
      alamat: '',
      rt: '',
      rw: '',
      penghasilanSebelumPandemi: '',
      penghasilanSetelahPandemi: '',
      alasan: '',
      terms: false,
      showModal: false,
      delay: null,
      isSuccess: false
    }
  },
  components: { Modal },
  methods: {
    handleSubmit() {
      this.delay = 1000 + Math.random() * 1000
      if (this.delay <= 1500) {
        this.isSuccess = true
      }
      this.showModal = true
    },
    toggleModal() {
      this.showModal = !this.showModal
    },
  }
}
</script>

<style>
  form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select, textarea {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  .container {
    display: flex;
    flex-direction: row;
    place-items: flex-start baseline;
    align-items: baseline;
    text-align: justify;
    text-justify: inter-word;
  }
  button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }
  .submit {
    text-align: center;
  }
  input[type=file]::file-selector-button {
    margin-right: 20px;
    border: none;
    background: #084cdf;
    padding: 8px 16px;
    border-radius: 4px;
    color: #fff;
    cursor: pointer;
    transition: background .2s ease-in-out;
  }
  input[type=file]::file-selector-button:hover {
    background: #0d45a5;
  }
  select {
    appearance: none;
    -webkit-appearance: none;
    font-size: 1em;
    padding: 0.675em 6em 0.675em 1em;
    background-color: #fff;
    cursor: pointer;
  }
</style>