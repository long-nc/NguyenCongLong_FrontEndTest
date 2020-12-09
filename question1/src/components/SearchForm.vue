<template>
  <div class="form-container">
    <FilterCombobox v-for="(filterValue, idx) in filterValues"
                    :key="filterValue.name" @change="filter => models[idx] = filter"
                    :label="filterValue.name" :items="filterValue.value" />
    <b-button style="color: white; font-weight: bold; margin-bottom: 8px"
              @click="search"
              class="align-self-end"
              variant="warning">
              Lọc tin
    </b-button>
  </div>
</template>

<script>
import FilterCombobox from './FilterCombobox'
import quan_huyen from '../data/quan_huyen'
import tinh_tp from '../data/tinh_tp'
import area from '../data/area'
import price from '../data/price'

export default {
  name: 'SearchForm',
  components: {FilterCombobox},
  data() {
    return {
      filterValues: [
        {
          name: 'Tỉnh thành',
          value: Object.keys(tinh_tp).map(key => ({text: tinh_tp[key].name, key: tinh_tp[key].code, value: tinh_tp[key]})),
        },
        {
          name: 'Quận huyện',
          value: Object.keys(quan_huyen).map(key => ({text: quan_huyen[key].name, key: quan_huyen[key].code, value: quan_huyen[key]}))
        },
        {
          name: 'Khoảng giá',
          value: price
        },
        {
          name: 'Diện tích',
          value: area
        }
      ],
      models: [ null, null, null, null],
    }
  },
  methods: {
    search() {
      this.$emit("search", this.models)
    }
  }
}
</script>

<style scoped>
  .form-container {
    border-radius: 4px;
    background-color: orange;
    display: flex;
    padding: 12px;
    margin: 0 36px;
  }
</style>