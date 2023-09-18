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
    <label for="nama">Nama:</label>
    <input type="text" id="nama" v-model="formInput.nama" placeholder="John Doe" required>

    <label for="nik">NIK:</label>
    <input type="number" id="nik" v-model="formInput.nik" placeholder="345678912398" required>

    <label for="noKk">Nomor Kartu Keluarga:</label>
    <input type="number" id="noKk" v-model="formInput.noKk" placeholder="345678912398" required>

    <label for="fotoKtp">Foto KTP:</label>
    <input type="file" id="noKtp" required>

    <label for="fotoKk">Foto Kartu Keluarga:</label>
    <input type="file" id="fotoKk" required>

    <label for="umur">Umur (tahun):</label>
    <input type="number" id="umur" v-model="formInput.umur" placeholder="25" required>

    <label for="jenisKelamin">Jenis Kelamin:</label>
    <select v-model="formInput.jenisKelamin" id="jenisKelamin" required>
      <option v-for="item in JenisKelaminEnum" :key="item">{{ item }}</option>
    </select>

    <label for="provinsi">Provinsi:</label>
    <select v-model="formInput.provinsi" id="provinsi" @change="onSelectProvince($event)" required>
      <option v-for="province in provinces" :key="province" :value="province.id">{{ province.name }}</option>
    </select>

    <div v-if="formInput.provinsi !== ''">
      <label for="kab">Kab/Kota:</label>
      <select v-model="formInput.kabupaten" id="kab" @change="onSelectRegency($event)" required>
        <option v-for="regency in regencies" :key="regency" :value="regency.id">{{ regency.name }}</option>
      </select>
    </div>

    <div v-if="formInput.kabupaten !== ''">
      <label for="kec">Kecamatan:</label>
      <select v-model="formInput.kecamatan" id="kec" @change="onSelectDistrict($event)" required>
        <option v-for="district in districts" :key="district" :value="district.id">{{ district.name }}</option>
      </select>
    </div>

    <div v-if="formInput.kecamatan !== ''">
      <label for="kel">Kelurahan/Desa:</label>
      <select v-model="formInput.kelurahan" id="kel" required>
        <option v-for="village in villages" :key="village" :value="village.id">{{ village.name }}</option>
      </select>
    </div>

    <label for="alamat">Alamat:</label>
    <textarea required v-model="formInput.alamat" id="alamat" placeholder="Jl Merdeka"></textarea>

    <label for="rt">RT:</label>
    <input type="number" required v-model="formInput.rt" id="rt" placeholder="04">

    <label for="rw">RW:</label>
    <input type="number" required v-model="formInput.rw" id="rw" placeholder="04">

    <label for="sblmPandemi">Penghasilan sebelum pandemi:</label>
    <input type="number" required v-model="formInput.penghasilanSebelumPandemi" id="sblmPandemi" placeholder="1.000.000">

    <label for="stlhPandemi">Penghasilan setelah pandemi:</label>
    <input type="number" required v-model="formInput.penghasilanSetelahPandemi" id="stlhPandemi" placeholder="1.000.000">

    <label for="alasan">Alasan membutuhkan bantuan:</label>
    <input type="text" required v-model="formInput.alasan" id="alasan" placeholder="Jobless">

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
import { reactive } from "vue";
import { JenisKelaminEnum } from '@/enums'
import Modal from './Modal.vue'

const formInput = reactive({
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
});

export default {
  data() {
    return {
      formInput,
      terms: false,
      showModal: false,
      delay: null,
      isSuccess: false,
      JenisKelaminEnum,
      provinces: [],
      regencies: [],
      districts: [],
      villages: []
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
    onSelectProvince(event) {
      var idProv = event.target.value
      fetch(`http://www.emsifa.com/api-wilayah-indonesia/api/regencies/${idProv}.json`)
        .then(response => response.json())
        .then(regencies => this.regencies = regencies);
    },
    onSelectRegency(event) {
      var idKab = event.target.value
      fetch(`http://www.emsifa.com/api-wilayah-indonesia/api/districts/${idKab}.json`)
        .then(response => response.json())
        .then(districts => this.districts = districts);
    },
    onSelectDistrict(event) {
      var idKec = event.target.value
      fetch(`http://www.emsifa.com/api-wilayah-indonesia/api/villages/${idKec}.json`)
        .then(response => response.json())
        .then(villages => this.villages = villages);
    }
  },
  mounted() {
    fetch(`http://www.emsifa.com/api-wilayah-indonesia/api/provinces.json`)
      .then(response => response.json())
      .then((provinces) => this.provinces = provinces);
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