<template>
  <div class="backdrop" v-if="showModal" @click.self="closeModal">
    <div class="modal">
      <div class="actions">
        <slot name="details"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showModal: false,
    }
  },
  methods: {
    closeModal() {
      this.$emit('close')
    }
  },
  mounted() {
    setTimeout(() => {
      this.showModal = true
    }, this.delay)    
  },
}
</script>

<style>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 10px;
  }
  .backdrop {
    top: 0;
    position: fixed;
    background: rgba(0,0,0,0.5);
    width: 100%;
    height: 100%;
  }
  .modal h1 {
    color: #03cfb4;
    border: none;
    padding: 0;
  }
  .modal p {
    font-style: normal;
    margin-bottom: 40px;
  }
  .modal .actions {
    text-align: center;
    margin: 30px 0 10px 0;
  }
  .modal .actions a {
    color: #333;
    padding: 8px;
    border: 1px solid #eee;
    border-radius: 4px;
    text-decoration: none;
    margin: 30px;
  }
</style>