<template>
  <!-- navbar -->
  <nav class="bg-gray-800 hidden lg:block">
    <div class="container">
      <div class="flex">
        <!-- all category -->
        <div class="px-8 py-4 bg-primary flex items-center cursor-pointer group relative">
          <span class="text-white">
            <i class="fas fa-bars"></i>
          </span>
          <span class="capitalize ml-2 text-white">All categories</span>

          <div
            class="absolute left-0 top-full w-full bg-white shadow-md py-3 invisible opacity-0 group-hover:opacity-100 group-hover:visible transition duration-300 z-50 divide-y divide-gray-300 divide-dashed"
          >
            <!-- single category -->
            <!-- <RouterLink
              class="px-6 py-3 flex items-center hover:bg-gray-100 transition"
              v-for="link in linkList"
              :key="link.id"
              :to="link.url"
            >
              <img :src="link.image" class="w-5 h-5 object-contain" />
              <span class="ml-6 text-gray-600 text-sm">{{ link.name }}</span>
            </RouterLink> -->
            <RouterLink
              class="px-6 py-3 flex items-center hover:bg-gray-100 transition"
              v-for="link in categoryList"
              :key="link.id"
              to="/product"
            >
              <img :src="link.thumbnail_url" class="w-5 h-5 object-contain" />
              <span class="ml-6 text-gray-600 text-sm">{{ link.name }}</span>
            </RouterLink>
            <!-- single category end -->
          </div>
        </div>
        <!-- all category end -->

        <!-- nav menu -->
        <div class="flex items-center justify-between flex-grow pl-12">
          <div class="flex items-center space-x-6 text-base capitalize">
            <RouterLink to="/" class="text-gray-200 hover:text-white transition">Home</RouterLink>
            <RouterLink to="/product" class="text-gray-200 hover:text-white transition">Product</RouterLink>
            <RouterLink to="/about-us" class="text-gray-200 hover:text-white transition">About us</RouterLink>
            <RouterLink to="/contact-us" class="text-gray-200 hover:text-white transition">Contact us</RouterLink>
          </div>
          <div
            v-if="isNotAuthPageAndNotAuthenticated"
            class="ml-auto justify-self-end text-gray-200 hover:text-white transition cursor-pointer"
            @click="handleLogin"
          >
            Login/Register
          </div>
          <div
            v-if="isAuthenticated"
            class="ml-auto justify-self-end text-gray-200 hover:text-white transition cursor-pointer"
            @click="handleLogout"
          >
            Logout
          </div>
        </div>
        <!-- nav menu end -->
      </div>
    </div>
  </nav>
  <!-- navbar end -->
</template>

<script setup lang="ts">
import bed from '@/assets/images/icons/bed.svg'
import sofa from '@/assets/images/icons/sofa.svg'
import office from '@/assets/images/icons/office.svg'
import terrace from '@/assets/images/icons/terrace.svg'
import bed2 from '@/assets/images/icons/bed-2.svg'
import restaurant from '@/assets/images/icons/restaurant.svg'
import { computed, onMounted, ref } from 'vue'
import router from '@/router'
import CategoryProps from '@/interfaces/category'
import CardProps from '@/interfaces/card'

const cardList = ref<CardProps[]>([])
const categoryList = ref<CategoryProps[]>([])
const filteredCardList = ref<CardProps[]>([])


import { useAuth } from '@/store/authStore'
import { isEmpty } from 'lodash'
import ProductAPI from '@/api/product.api'
const authStore = useAuth()

const user = (localStorage.getItem('auth') && (JSON.parse(localStorage.getItem('auth') || '') as any)) || {}
const isAuthenticated = !isEmpty(user)
// console.log('isAuthenticated',isAuthenticated, 'user', JSON.parse(localStorage.getItem('auth') || ''))

const url = computed(() => window.location.href)
// ADD MORE AUTH ROUTE NAME HERE
const isNotAuthPage = computed(() => !(url.value.includes('login') || url.value.includes('signup')))

const isNotAuthPageAndNotAuthenticated = computed(() => !isAuthenticated && isNotAuthPage.value)

const handleLogin = () => {
  router.push('/login')
}

const handleLogout = () => {
  authStore.logout()
  localStorage.removeItem('auth')
  localStorage.removeItem('user')
  localStorage.removeItem('token')
  router.push('/login')
}

const linkList = ref([
  {
    id: '1',
    url: '/filter?category=bed',
    image: bed,
    name: 'Bedroom'
  },
  {
    id: '2',
    url: '/filter?category=sofa',
    image: sofa,
    name: 'Sofa'
  },
  {
    id: '3',
    url: '/filter?category=office',
    image: office,
    name: 'Office'
  },
  {
    id: '4',
    url: '/filter?category=terrace',
    image: terrace,
    name: 'Terrace'
  },
  {
    id: '5',
    url: '/filter?category=bed',
    image: bed2,
    name: 'Bedroom'
  },
  {
    id: '6',
    url: '/filter?category=restaurant',
    image: restaurant,
    name: 'Restaurant'
  }
])


onMounted(async () => {
  try {
    const res = await ProductAPI.getCategory({
      page_no: 1,
      per_page: 10
    })
    categoryList.value = res?.data?.list
  } catch (error) {
    console.error('Error fetching data:', error)
  }
  try {
    const res = await ProductAPI.getRecommendProduct({
      page_no: 1,
      per_page: 149
    })
    cardList.value = res?.data?.list
    filteredCardList.value = cardList.value // Hiển thị tất cả sản phẩm ban đầu
  } catch (error) {
    console.error('Error fetching data:', error)
  }
})
</script>
