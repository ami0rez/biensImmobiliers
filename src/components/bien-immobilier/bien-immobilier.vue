<script setup>
import { ref, onMounted, computed } from 'vue';
import { defineComponent } from "vue";


import BienImmobilierSearchComponent from "./bien-immobilier-search.vue";
import BienImmobilierDetailsComponent from "./bien-immobilier-details.vue";

import { useAssetStore } from "../../stores/asset";

const store = useAssetStore();


const filteredAssets = computed(() => {
  return store.getSearchAssets
})
const assetOptions = computed(() => {
  return store.getAssetOptions
})
const details = computed(() => {
  return store.getDetails
})


onMounted(() => {
  store.fetchAssets();
})
</script>
<script>
export default {
  name: "BienImmobilier",
  setup(props) {
    const store = useAssetStore();
    return {}
  },
  methods: {
    refreshResults(value) {
      this.store.filterAssets(value)
      this.store.setDetails(undefined)
    },
    showDetails(value) {
      this.store.setDetails(value)
    }
  }
}

</script>
<template>
  <div class="bien-imm-container">
    <BienImmobilierSearchComponent @search="refreshResults" :options="assetOptions" />
    <DataTable v-if="filteredAssets?.length" class="mb-20c p-datatable-sm" :value="filteredAssets"  :paginator="true" :rows="10"
      paginatorTemplate="CurrentPageReport FirstPageLink PrevPageLink PageLinks NextPageLink LastPageLink RowsPerPageDropdown"
      :rowsPerPageOptions="[10,20,50]" responsiveLayout="scroll"
      currentPageReportTemplate="Affichage de {first} à {last} a partire de {totalRecords}">
      <Column field="address_line1" header="Addresse Ligne 1"></Column>
      <Column field="ville" header="Ville"></Column>
      <Column field="type" header="Type"></Column>
      <Column field="prix" header="Prix"></Column>
      <Column header="Details">
        <template #body="slotProps">
          <i class="pi pi-search c-pointer" @click="showDetails(slotProps.data)"></i>
        </template>
      </Column>
    </DataTable>
    <BienImmobilierDetailsComponent v-if="details" :value="details" />
  </div>
</template>



<style>
.bien-imm-container {
  display: flex;
  flex-direction: column;
}
</style>