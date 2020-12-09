<template>
  <div class="combobox-container d-flex flex-column">
    <span class="label align-self-start">{{label}}</span>
    <b-dropdown :text="value ? value.text : label" class="m-md-2" variant="light">
      <input v-model="searchText" />
      <b-dropdown-item disabled>{{label}}</b-dropdown-item>
      <b-dropdown-item v-for="item in internalItems" :key="item.key" :value="item.value" @click="onChangeItem(item)">
        {{item.text}}
      </b-dropdown-item>
    </b-dropdown>
  </div>
</template>

<script>

export default {
  name: 'FilterCombobox',
  props: ['label', 'items'],
  data() {
    return {
      value: null,
      internalItems: [],
      searchText: ''
    }
  },
  created() {
    this.internalItems = this.items
  },
  methods: {
    onChangeItem(item) {
      this.value = item
      this.$emit("change", item)
    }
  },
  watch: {
    searchText(searchKeyword) {
      if (searchKeyword) {
        this.internalItems = this.items.filter(item => item.text.toLowerCase().includes(searchKeyword.toLowerCase()))
      }
    }
  }
}
</script>

<style scoped>
  .label {
    font-weight: bold;
  }

  .combobox-container {
    min-width: 160px;
    margin-right: 16px;
  }
</style>