<template>
  <Slider />
  <Categories />
  <RecommendedServices />
</template>

<script>

import Slider from '../components/home/slider.vue'
import Categories from '../components/categories/categories_grid.vue'
// import FeaturedCategories from '../components/home/featured_categories.vue'
import RecommendedServices from '../components/home/recommended_services.vue'

export default {
  components: {
    Slider,
    Categories,
    // FeaturedCategories,
    RecommendedServices,
  },
}
</script>
