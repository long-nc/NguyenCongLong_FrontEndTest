<template>
  <div class="d-flex flex-column">
    <search-form @search="filterPosts" />
    <div style="margin-top: 36px" class="align-self-stretch">
      <post-container :posts="posts" />
    </div>
  </div>
</template>

<script>
import SearchForm from './SearchForm'
import PostContainer from './PostContainer'

import postData from '../data/data'
import quan_huyen from '../data/quan_huyen'
import tinh_tp from '../data/tinh_tp'

import _ from 'lodash'

const FILTER_CITY = 0;
const FILTER_DISTRICT = 1;
const FILTER_PRICE = 2;
const FILTER_AREA = 3;

export default {
  name: 'Container',
  components: {
    SearchForm, PostContainer
  },
  data() {
    return {
      posts: []
    }
  },
  methods: {
    formatPrice(price) {
      if (price > 1000000) {
        return price / 1000000 + " triệu/tháng"
      } else {
        return price / 1000 + " k/tháng"
      }
    },
    formatAddress(district) {
      return _.get(quan_huyen[district], 'path_with_type', '');
    },
    filterPrice(priceCategory) {
      switch (priceCategory) {
        case "duoi_1_trieu":
          return post => post.price < 1000000
        case "1_2_trieu":
          return post => post.price >= 1000000 && post.price < 2 * 1000000
        case "2_3_trieu":
          return post => post.price >= 2 * 1000000 && post.price < 3 * 1000000
        case "3_5_trieu":
          return post => post.price >= 3 * 1000000 && post.price < 5 * 1000000
        case "5_7_trieu":
          return post => post.price >= 5 * 1000000 && post.price < 7 * 1000000
        case "7_10_trieu":
          return post => post.price >= 7 * 1000000 && post.price < 10 * 1000000
        case "10_15_trieu":
          return post => post.price >= 10 * 1000000 && post.price < 15 * 1000000
        case "tren_15_trieu":
          return post => post.price >= 15 * 1000000
      }
    },
    filterArea(areaCategory) {
      switch (areaCategory) {
        case "duoi_20_m2":
          return post => post.area < 20
        case "20m2_30m2":
          return post => post.area >= 20 && post.area < 30
        case "30m2_50m2":
          return post => post.area >= 30 && post.area < 50
        case "50m2_60m2":
          return post => post.area >= 50 && post.area < 60
        case "60m2_70m2":
          return post => post.area >= 60 && post.area < 70
        case "70m2_80m2":
          return post => post.area >= 70 && post.area < 80
        case "80m2_90m2":
          return post => post.area >= 80 && post.area < 90
        case "90m2_100m2":
          return post => post.area >= 90 && post.area < 100
        case "tren_100_m2":
          return post => post.area >= 100
      }
    },
    filterPosts(categories) {
      const self = this;
      const filters = categories.map((category, idx) => {
        if (category) {
          switch (idx) {
            case FILTER_CITY:
              return post => post.city === category.value.code;
            case FILTER_DISTRICT:
              return post => post.district === category.value.code;
            case FILTER_PRICE:
              return self.filterPrice(category.value);
            case FILTER_AREA:
              return self.filterArea(category.value);
          }
        }
        return null
      }).filter(f => f)

      
      this.posts = filters.reduce((filteredData, func) => filteredData.filter(func), postData)
                   .map(p => ({
                      ...p,
                      content: p.content.substring(0, 200),
                      formattedPrice: self.formatPrice(p.price),
                      formattedAddress: self.formatAddress(p.district),
                      formattedArea: p.area + "m²"
                    }))
    }
  },
  created() {
    const self = this
    this.posts = postData.map(p => ({
      ...p,
      content: p.content.substring(0, 200),
      formattedPrice: self.formatPrice(p.price),
      formattedAddress: self.formatAddress(p.district),
      formattedArea: p.area + "m²"
    }))
  }
}
</script>