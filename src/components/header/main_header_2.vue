<template>
  <div class="main_header">
    <div class="header_wrapper">
        <div class="drawer_icon">
        <MenuIcon
            v-if='!open'
            aria-hidden='true'
            class='block w-6 h-6'
        />
        <XIcon
            v-else
            class="block"
            aria-hidden='true'
        />
        <router-link to="/"><img
            :alt='this.$settings["app_name"]'
            :src='this.$settings["app_logo"]'
            class='logo'
            /></router-link>
        <span class='mx-3 lg:block hidden font-bold text-second-color-600'>{{ this.$settings['app_name'] }}</span>
        <router-link
            :class="{'border-main-color-500 text-white font-bold': ($router.currentRoute.value.name === 'Categories'),'border-transparent text-black-500 hover:border-gray-300 hover:text-gray-700': ($router.currentRoute.value.name !== 'Categories')}"
            class='lg:block hidden inline-flex  items-center px-1 pt-1 text-sm font-medium border-b-2 '
            to='/categories'
        >
            {{ $t('Categories') }}
        </router-link>

        </div>
        <search-bar v-if="is_searchComp"/>
        <div class="icons">
        <div
            class="notification"
            v-if='this.isAuth'
        >
            <BellIcon />
            <span>3</span>
        </div>

        <router-link v-if='!this.isAuth' :to='{name:"Login"}' class='profile' >
            <UserIcon/>
        </router-link>
        <router-link v-if='!this.isAuth' :to='{name:"Login"}'
            class='hidden text-sm md:inline-flex focus:outline-none text-second-color-500 hover:text-second-color-900'
            type='button'>
            {{ $t('Login') }}
            </router-link>
            <router-link v-if='!this.isAuth' :to='{name:"Register"}'
            class='hidden px-4 py-2 text-sm text-white rounded-md border border-transparent shadow-sm md:inline-flex bg-main-color-600 hover:bg-main-color-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-main-color-500'
            type='button'>
            {{ $t('Register') }}
            </router-link>
        </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { BellIcon, MenuIcon, XIcon, SearchIcon , UserIcon } from '@heroicons/vue/outline'
import { PlusIcon } from '@heroicons/vue/solid'
import MyAddresses from './my_addresses.vue'
import AddressPicker from './address_picker.vue'
import MyNotifications from './my_notifications.vue'
// import Languages from './languages.vue'
import Profile from './profile.vue'
import { mapGetters, mapActions } from 'vuex'
import SearchBar from '../home/partial/search_bar.vue'

export default {
	components: {
		// Languages,
		MyNotifications,
		MyAddresses,
        UserIcon,
		SearchIcon,
		Profile,
		AddressPicker,
		Disclosure,
		DisclosureButton,
		DisclosurePanel,
		Menu,
		MenuButton,
		MenuItem,
		MenuItems,
		BellIcon,
		MenuIcon,
		XIcon,
		SearchBar,
	},
	setup() {
		const open = ref(false)

		return {
			open,
		}
	},
	computed: {
		is_searchComp() {
			if (this.$route.name !== 'Search' && this.$route.name !== 'help') {
				return true
			}
		},
		...mapGetters('user', ['getUser', 'isAuth']),
	},
	methods: {
		...mapActions('user', ['logoutAction', 'toggleProfileAction']),
		...mapActions('snackbar', ['toggleSnackBarAction']),
		async logout() {
			const result = this.logoutAction()
			await this.$router.replace({ name: 'Home' })
			this.toggleSnackBarAction(result)
		},
	},
}
</script>


<style>
.main_header {
	background-color: #2596be;
	position: sticky;
	padding: 10px 1rem;
	width: 100%;
}
.header_wrapper{
    display: flex;
	justify-content: space-between;
	align-items: center;
}
.drawer_icon {
	display: flex;
	align-items: center;
}
.drawer_icon svg {
	color: #fff;
	margin-right: 10px;
}
.logo {
	max-height: 40px;
}

.icons svg {
	max-width: 40px;
}
.notification {
	position: relative;
}
.notification span {
	position: absolute;
	bottom: 0;
	right: 0;
	background-color: orange;
	width: 20px;
	height: 20px;
	border-radius: 50%;
	display: flex;
	justify-content: center;
	align-items: center;
	color: #fff;
}
.profile svg{
    max-height: 40px;
    color:#fff
}

@media (min-width: 600px) {
	.drawer_icon svg {
		display: none;
	}
   
}
@media (min-width: 766px) {
    .profile{
        display: none;
    }
}
</style>