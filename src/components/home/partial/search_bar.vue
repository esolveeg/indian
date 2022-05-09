<template>
 <div class="search">
        <SearchIcon @click.prevent="goToSearchPage" class="search_icon cursor-pointer" />
        <input
            class="search_input"
            
            :placeholder="$t('Search')"
            @keyup.enter="goToSearchPage"
            :value='keywords'
            type='text'
             @input='search'
        >
        <router-link :to='{name:"Search",params:{keywords:keywords}}'>{{ $t('Search') }}</router-link>
        </div>
  
</template>

<script>
import { mapState, mapActions } from 'vuex'
import {  SearchIcon } from '@heroicons/vue/outline'

export default {
  name: 'SearchBar',
  components:{
    SearchIcon
  },
  computed: {
    ...mapState('eService', {
      keywords: state => state.keywords,
    }),
  },
  mounted() {
    this.updateKeywordsAction(undefined)
  },
  methods: {
    ...mapActions('eService', [
      'updateKeywordsAction',
    ]),
    goToSearchPage(){
      this.$router.push({name:'Search',params:{keywords:this.keywords}})
    },
    search(e) {
      this.updateKeywordsAction(e.target.value)
    },
  },
}

</script>

<style >

.search input {
	border-radius: 15px;
	min-height: 50px;
	padding: 0 20px 0 50px;
	max-width: 100%;
}
.search {
	position: relative;
}
.search a{
    position: absolute;
    right: 5px;
    border-radius: 15px;
    background-color: #2596be;
    color: #fff;
    width: 100px;
    height: 40px;
    top: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.search_icon {
	max-width: 30px;
	position: absolute;
	left: 10px;
	top: 10px;
	color: #2596be;
}

@media (max-width: 766px) {
	.search {
		max-width: 250px;
	}
    .search a{
        display: none;
    }
}

@media (max-width: 400px) {
	.search {
		max-width: 150px;
	}
}
</style>