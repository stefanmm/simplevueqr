<template>
<div id="qrholder" class="container is-max-desktop">
  <div class="columns is-mobile">
    <div class="column is-half is-offset-one-quarter">

        <div class="card">
          <div class="card-image p-5">
            <figure class="image is-1by1">
            
              <img :src="(imgQrUrl != '') ? imgQrUrl : require('@/assets/waiting.jpg')" />
              
            </figure>
          </div>
          <form class="submitNew" @submit.prevent="createNewQr">
          <div class="card-content">
            <div class="media">
              <div class="media-left">
                <figure class="image is-40x40">
                  <img src="@/assets/list.png" alt="Placeholder image">
                </figure>
              </div>
              
              <div class="media-content">
                <div class="field ">
                  <div class="control ">

                    <div class="select is-info is-fullwidth">
                      <select class="" id="QrType" v-model="selectedType">
                        <option :value='qrType.value' v-for='(qrType, index) in qrTypes' :key='index'>
                         <span>{{ qrType.name }}</span>
                        </option>
                      </select>
                    </div>

                  </div>
                </div>
              </div>
            </div>

            <div class="content">
              <div class="field">
              <div class="control">
                <textarea id="newQrInput" class="textarea is-info" rows="4" placeholder="Enter text..." v-model="newQrInput" v-if='selectedType == "raw"' required />
                <input id="newQrInputUrl" class="input is-info" type="url" placeholder="Enter URL..." v-if='selectedType == "url"' v-model="newQrInput" required />
               <input id="newQrInputPhone" class="input is-info" type="tel" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" placeholder="Enter phone number (eg. 123-456-7890)" v-model="newQrInput" v-if='selectedType == "phone"' required />
              </div>
              </div>
              <button type="submit" class="button is-info is-fullwidth"  icon-right="delete"><b-icon icon="qrcode" class="mr-2"></b-icon> GENERATE</button>
            </div>
          </div>
          </form>
        </div>
 
    </div>
  </div>

</div>
</template>

<script>

export default {
  
  name: 'NewQr',
  
  data() {
    return {
     imgQrUrl: "",
      newQrInput: "",
      selectedType: "raw",
      qrTypes: [
        {value: 'raw', name: 'Raw (text)'},
        {value: 'url', name: 'URL'},
        {value: 'phone', name: 'Phone Number'}
      ]
    }
  },
  methods: {
    createNewQr(){
      var userInput = this.newQrInput;
      if(userInput) {
       if(this.selectedType == "phone") {
         this.imgQrUrl = 'https://api.qrserver.com/v1/create-qr-code/?data='+escape("tel:"+userInput)+'&size=420x420';
       } else {
          this.imgQrUrl = 'https://api.qrserver.com/v1/create-qr-code/?data='+escape(userInput)+'&size=420x420';
       }
       
        this.newQrInput = "";
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
