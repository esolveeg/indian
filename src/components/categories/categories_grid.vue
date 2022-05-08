<template>
  <div class='px-4 py-20 bg-gray-100 sm:px-0'>
    <CategoriesLoader v-if='allCategoriesWithSubcategories.length === 0' />
    <div v-else class='overflow-hidden gap- mx-auto max-w-7xl sm:px-6 lg:px-8 sm:grid-cols-2 md:grid-cols-2 sm:gap-8'>
      <tabs :options="{ useUrlFragment: false }" @clicked="tabClicked" @changed="tabChanged" nav-item-class="nav-item">
        <tab v-for='category in allCategoriesWithSubcategories' :key='category.id'  :name="$filters.transString(category?.name)">
           <SubCategories :subCategories='category?.sub_categories || []' aria-hidden='true' />
        </tab>
    </tabs>
    </div>
  </div>

</template>

<script>
import { createNamespacedHelpers } from 'vuex'
import {Tabs, Tab} from 'vue3-tabs-component';
const { mapState, mapActions } = createNamespacedHelpers('category')

import SubCategories from './sub_categories.vue'
import CategoriesLoader from './partial/categories_loader.vue'

export default {
  components: { CategoriesLoader, SubCategories , Tabs ,Tab },
  mounted() {
    this.getAllWithSubCategoriesAction()
  },
  computed: {
    ...mapState(['allCategoriesWithSubcategories']),
  },
  methods: {
    ...mapActions(['getAllWithSubCategoriesAction']),
  },
}
</script>

<style>
.tabs-component-tabs{
  display: flex;
  justify-content: center;
}
.tabs-component-tabs li a{
  width: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 25px;
  background-color: #fbe9e7;
  height: 50px;
  color: #000;
  font-weight: 500;
  font-size: 18px;
  transition: all .3s;
}
.tabs-component-tabs li.is-active a{
  background-color: #2596be;
  color: #fff;
}
.tabs-component-tabs li:not(:first-child){
  transform: translateX(-35px);
}
</style>