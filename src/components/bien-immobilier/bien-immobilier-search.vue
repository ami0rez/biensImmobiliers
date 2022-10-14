<template>
  <div class="bien-imm-search-container">
    <div class="search-item">
      Estimer un bien
    </div>
    <AutoComplete 
      type="text" 
      class="search-item search-item-input"
      v-model="value" 
      :options="options" 
    />
    <Button label="Rechercher" icon="pi pi-check" iconPos="right" @click="() => search()" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props:['options'],
  name: "BienImmobilierSearchComponent",
  setup() {
    return {
      value: null,
      filteredCountriesBasic:[]
    };
  },
  methods: {
		searchCountry(event: any) {
      this.filteredCountriesBasic = this.options.filter(option => option.label.includes(event.query));
      
		},
    search(){
      this.$emit('search', this.value)
    }
	}
});
</script>

<style>
.bien-imm-search-container {
  display: flex;
  flex-direction: row;
  justify-content: baseline;
  align-items: center;
  margin: 10px 0 20px 0;
}
.bien-imm-search-container .search-item {
  margin-right: 20px;
}
.search-item-input{
  width: 400px;
}
</style>