<template>
  <div class="bien-imm-details-container">
    <div class="bien-imm-details-box m-10-20">
      <div class="bien-imm-details-item">
        Addresse : {{value?.address_line1}}
      </div>
      <div class="bien-imm-details-item">
        Ville : {{value?.ville}}
      </div>
      <div class="bien-imm-details-item">
        Type : {{value?.type}}
      </div>
      <div class="bien-imm-details-item">
        Details : {{value?.description}}
      </div>
      <div class="bien-imm-details-item f-grow flex-bottom-end">
        Prix : {{value?.prix}}
      </div>
    </div>
    <div class="bien-imm-details-box border-round flex-center m-10-20">
      <img :src="value?.photo" alt="Photo">
    </div>
  </div>
  
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  props:['value'],
  name: "BienImmobilierDetailsComponent",
  setup() {
   
  },
});
</script>

<style>
.bien-imm-details-container {
  display: flex;
  flex-direction: row;
}
.bien-imm-details-box {
  width: 50%;
  height: 200px;
  border: solid thin #00000033;
  display: flex;
  flex-direction: column;
  padding: 5px;
}
.bien-imm-details-item {
  height: 40px;
}
.bien-imm-details-image{
  border-radius: 20px;
}
</style>