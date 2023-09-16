<template>
  <form>
    <label>Nama:</label>
    <input type="text" required v-model="nama">

    <label>NIK:</label>
    <input type="number" required v-model="nik">

    <label>Nomor Kartu Keluarga:</label>
    <input type="number" required v-model="noKk">

    <label>Foto KTP:</label>
    <input type="file" required>

    <label>Foto Kartu Keluarga:</label>
    <input type="file" required>

    <label>Umur:</label>
    <input type="number" required v-model="umur">

    <label>Jenis Kelamin:</label>
    <select v-model="jenisKelamin">
      <option value="0">Laki-laki</option>
      <option value="1">Perempuan</option>
    </select>

    <label>Provinsi:</label>
    <input type="text" required v-model="provinsi">

    <label>Kab/Kota:</label>
    <input type="text" required v-model="kabupaten">

    <label>Kecamatan:</label>
    <input type="text" required v-model="kecamatan">

    <label>Kelurahan/Desa:</label>
    <input type="text" required v-model="kelurahan">

    <label>Alamat:</label>
    <input type="text" required v-model="alamat">

    <label>RT:</label>
    <input type="number" required v-model="rt">

    <label>RW:</label>
    <input type="number" required v-model="rw">

    <label>Penghasilan sebelum pandemi:</label>
    <input type="number" required v-model="penghasilanSebelumPandemi">

    <label>Penghasilan setelah pandemi:</label>
    <input type="number" required v-model="penghasilanSetelahPandemi">

    <label>Alasan membutuhkan bantuan:</label>
    <input type="number" required v-model="alasan">

    <div class="terms">
      <label><span>Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.</span></label>
    </div>

    <button>Submit</button>
  </form>
  <p>Jenis kelamin: {{ jenisKelamin }}</p>
</template>

<script>
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
      alasan: ''
    }
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
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  button {
    background: #0faf87;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }
  span {
    color: #ec5656;
  }
</style>