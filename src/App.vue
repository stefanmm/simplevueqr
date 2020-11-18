<template>
  <div id="app">
    <section class="hero is-info mb-6 has-text-centered	">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            QR Code Generator
          </h1>
          <h2 class="subtitle">
            Simple VUE.js QR code generator
          </h2>
        </div>
      </div>
    </section>
  
  <NewQr />
  <Footer />
  </div>
   
</template>

<script>
import NewQr from './components/NewQr'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    NewQr,
    Footer
    
  }
}
</script>

<style>
body, html {
  background-color: #363636!important;
}
</style>
