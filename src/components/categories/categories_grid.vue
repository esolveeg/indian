<template>
  <div class='px-4 py-20 bg-gray-100 sm:px-0'>
    <CategoriesLoader v-if='allCategoriesWithSubcategories.length === 0' />
    <div v-else class='overflow-hidden gap- mx-auto max-w-7xl sm:px-6 lg:px-8 sm:grid-cols-2 md:grid-cols-2 sm:gap-8'>
      <tabs :options="{ useUrlFragment: false }" @clicked="tabClicked" @changed="tabChanged" nav-item-class="nav-item">
        <tab v-for='category in allCategoriesWithSubcategories' :key='category.id'  :name="$filters.transString(category?.name)">
           <div class='grid overflow-hidden grid-cols-2 gap-4 px-4 mx-auto max-w-7xl sm:py-6 sm:px-6 lg:px-8 sm:grid-cols-3 lg:grid-cols-6 sm:gap-8'>
      <CategoryItem v-for='subcat in category.sub_categories' :key='subcat.id' :category='subcat' />
    </div>
        </tab>
    </tabs>
    </div>
  </div>

</template>

<script>
import { createNamespacedHelpers } from 'vuex'
import {Tabs, Tab} from 'vue3-tabs-component';
const { mapState, mapActions } = createNamespacedHelpers('category')
import CategoryItem from './partial/category_item.vue'

import SubCategories from './sub_categories.vue'
import CategoriesLoader from './partial/categories_loader.vue'

export default {
  components: { CategoriesLoader, CategoryItem , Tabs ,Tab },
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
  margin-bottom: 20px;
}
.tabs-component-tabs li a{
  /* width: 300px; */
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
  padding: 0 50px;
}
.tabs-component-tabs li.is-active a{
  background-color: #2596be;
  color: #fff;
  /* width: auto !important; */
}
.tabs-component-tabs li:not(:first-child){
  transform: translateX(-35px);
}
@media(max-width:500px){
  .tabs-component-tabs .nav-item a{
  padding: 0 40px;
  font-size: 12px;
    /* width: 200px !important; */
  }
}
@media(max-width:400px){
  .tabs-component-tabs .nav-item a{
    /* width: 180px !important; */
    font-size: 12px;
  }
}
@media(max-width:300px){
  .tabs-component-tabs .nav-item a{
    /* width: 120px !important; */
    font: 14px;
  }
}
</style>