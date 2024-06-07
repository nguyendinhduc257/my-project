<template>
  <!-- breadcrum -->
  <div class="container py-4 flex justify-between">
    <div class="flex gap-3 items-center">
      <a href="index.html" class="text-primary text-base">
        <i class="fas fa-home"></i>
      </a>
      <span class="text-sm text-gray-400"><i class="fas fa-chevron-right"></i></span>
      <p class="text-gray-600 font-medium">Shop</p>
    </div>
  </div>
  <!-- breadcrum end -->

  <!-- shop wrapper -->
  <div class="container grid lg:grid-cols-4 gap-6 pt-4 pb-16 items-start relative">
    <!-- sidebar -->
    <div
      class="col-span-1 bg-white px-4 pt-4 pb-6 shadow rounded overflow-hidden absolute lg:static left-4 top-16 z-10 w-72 lg:w-full lg:block">
      <div class="divide-gray-200 divide-y space-y-5 relative">
        <!-- category filter -->
        <div class="relative">
          <div class="lg:hidden text-gray-400 hover:text-primary text-lg absolute right-0 top-0 cursor-pointer">
            <i class="fas fa-times"></i>
          </div>
          <h3 class="text-xl text-gray-800 mb-3 uppercase font-medium">Categories</h3>
          <div class="space-y-2">
            <!-- single category -->
            <div class="flex items-center">
              <input :name="'categoryRadio'" type="radio" id="allCategory"
                class="text-primary focus:ring-0 rounded-lg cursor-pointer" @change="showAllProducts" />
              <label for="allCategory" class="text-gray-600 ml-3 cursor-pointer">Tất cả</label>
              <div class="ml-auto text-gray-600 text-sm">({{ cardList.length }})</div>
            </div>
            <div class="flex items-center" v-for="category in categoryList" id="category.id">
              <input :name="'categoryRadio'" type="radio" id="category.id"
                class="text-primary focus:ring-0 rounded-lg cursor-pointer" @change="filterByCategory(category.id)" />
              <label class="text-gray-600 ml-3 cursor-pointer">{{ category.name }}</label>
              <div class="ml-auto text-gray-600 text-sm">({{ category.products.length }})</div>
            </div>
            <!-- single category end -->

            <!-- single category end -->
          </div>
        </div>
        <!-- category filter end -->
        <!-- brand filter -->
        <div class="pt-4">
          <h3 class="text-xl text-gray-800 mb-3 uppercase font-medium">Brands</h3>
          <div class="space-y-2">
            <!-- single brand name -->
            <div class="flex items-center">
              <input type="checkbox" id="Dominik" class="text-primary focus:ring-0 rounded-sm cursor-pointer" />
              <label for="Dominik" class="text-gray-600 ml-3 cursor-pointer">Dominik</label>
              <div class="ml-auto text-gray-600 text-sm">(15)</div>
            </div>
            <!-- single brand name end -->
            <!-- single brand name -->
            <div class="flex items-center">
              <input type="checkbox" id="Karl" class="text-primary focus:ring-0 rounded-sm cursor-pointer" />
              <label for="Karl" class="text-gray-600 ml-3 cursor-pointer">Karl</label>
              <div class="ml-auto text-gray-600 text-sm">(18)</div>
            </div>
            <!-- single brand name end -->
            <!-- single brand name -->
            <div class="flex items-center">
              <input type="checkbox" id="Maxing" class="text-primary focus:ring-0 rounded-sm cursor-pointer" />
              <label for="Maxing" class="text-gray-600 ml-3 cursor-pointer">Maxing</label>
              <div class="ml-auto text-gray-600 text-sm">(09)</div>
            </div>
            <!-- single brand name end -->
            <!-- single brand name -->
            <div class="flex items-center">
              <input type="checkbox" id="Ernest" class="text-primary focus:ring-0 rounded-sm cursor-pointer" />
              <label for="Ernest" class="text-gray-600 ml-3 cursor-pointer">Ernest</label>
              <div class="ml-auto text-gray-600 text-sm">(12)</div>
            </div>
            <!-- single brand name end -->
          </div>
        </div>
        <!-- brand filter end -->
        <!-- price filter -->
        <div class="pt-4">
          <h3 class="text-xl text-gray-800 mb-3 uppercase font-medium">Price</h3>
          <div class="mt-4 flex items-center">
            <input type="text"
              class="w-full border-gray-300 focus:ring-0 focus:border-primary px-3 py-1 text-gray-600 text-sm shadow-sm rounded"
              placeholder="min" />
            <span class="mx-3 text-gray-500">-</span>
            <input type="text"
              class="w-full border-gray-300 focus:ring-0 focus:border-primary px-3 py-1 text-gray-600 text-sm shadow-sm rounded"
              placeholder="mix" />
          </div>
        </div>
        <!-- price filter end -->
        <!-- size filter -->
        <div class="pt-4">
          <h3 class="text-xl text-gray-800 mb-3 uppercase font-medium">size</h3>
          <div class="flex items-center gap-2">
            <div class="size-selector">
              <input type="radio" name="size" class="hidden" id="size-xs" />
              <label for="size-xs"
                class="text-xs border border-gray-200 rounded-sm h-6 w-6 flex items-center justify-center cursor-pointer shadow-sm text-gray-600">
                XS
              </label>
            </div>
            <div class="size-selector">
              <input type="radio" name="size" class="hidden" id="size-s" />
              <label for="size-s"
                class="text-xs border border-gray-200 rounded-sm h-6 w-6 flex items-center justify-center cursor-pointer shadow-sm text-gray-600">
                S
              </label>
            </div>
            <div class="size-selector">
              <input type="radio" name="size" class="hidden" id="size-m" checked />
              <label for="size-m"
                class="text-xs border border-gray-200 rounded-sm h-6 w-6 flex items-center justify-center cursor-pointer shadow-sm text-gray-600">
                M
              </label>
            </div>
            <div class="size-selector">
              <input type="radio" name="size" class="hidden" id="size-l" />
              <label for="size-l"
                class="text-xs border border-gray-200 rounded-sm h-6 w-6 flex items-center justify-center cursor-pointer shadow-sm text-gray-600">
                L
              </label>
            </div>
            <div class="size-selector">
              <input type="radio" name="size" class="hidden" id="size-xl" />
              <label for="size-xl"
                class="text-xs border border-gray-200 rounded-sm h-6 w-6 flex items-center justify-center cursor-pointer shadow-sm text-gray-600">
                XL
              </label>
            </div>
          </div>
        </div>
        <!-- size filter end -->
        <!-- color filter -->
        <div class="pt-4">
          <h3 class="text-xl text-gray-800 mb-3 uppercase font-medium">color</h3>
          <div class="flex items-center gap-2">
            <div class="color-selector">
              <input type="radio" name="color" class="hidden" id="color-red" checked />
              <label for="color-red" style="background-color: #fc3d57"
                class="text-xs border border-gray-200 rounded-sm h-5 w-5 flex items-center justify-center cursor-pointer shadow-sm">
              </label>
            </div>
            <div class="color-selector">
              <input type="radio" name="color" class="hidden" id="color-white" />
              <label for="color-white" style="background-color: #fff"
                class="text-xs border border-gray-200 rounded-sm h-5 w-5 flex items-center justify-center cursor-pointer shadow-sm">
              </label>
            </div>
            <div class="color-selector">
              <input type="radio" name="color" class="hidden" id="color-black" />
              <label for="color-black" style="background-color: #000"
                class="text-xs border border-gray-200 rounded-sm h-5 w-5 flex items-center justify-center cursor-pointer shadow-sm">
              </label>
            </div>
          </div>
        </div>
        <!-- color filter end -->
      </div>
    </div>
    <!-- sidebar end -->

    <!-- products -->
    <div class="col-span-3">
      <!-- sorting -->
      <div class="mb-4 flex items-center">
        <button
          class="bg-primary border border-primary text-white px-10 py-3 font-medium rounded uppercase hover:bg-transparent hover:text-primary transition lg:hidden text-sm mr-3 focus:outline-none">
          Filter
        </button>
        <select
          class="w-44 text-sm text-gray-600 px-4 py-3 border-gray-300 shadow-sm rounded focus:ring-primary focus:border-primary"
          @change="sortProducts($event)">
          <option value="default">Default sorting</option>
          <option value="low-high">Price low-high</option>
          <option value="high-low">Price high-low</option>
          <option value="latest">Latest product</option>
        </select>
        <div class="flex gap-2 ml-auto">
          <div :class="'border border-gray-300 w-10 h-9 flex items-center justify-center text-gray-600 rounded cursor-pointer ' +
                [targetDisplayType === 'col' ? 'border border-primary text-white bg-primary' : '']
                " @click="handleChangeDisplayType('col')">
            <i class="fas fa-th"></i>
          </div>
          <div :class="'border border-gray-300 w-10 h-9 flex items-center justify-center text-gray-600 rounded cursor-pointer ' +
                [targetDisplayType === 'row' ? 'border border-primary text-white bg-primary' : '']
                " @click="handleChangeDisplayType('row')">
            <i class="fas fa-list"></i>
          </div>
        </div>
      </div>
      <!-- sorting end -->
      <!-- product wrapper -->
      <div v-if="targetDisplayType === 'col'" class="grid lg:grid-cols-2 xl:grid-cols-3 sm:grid-cols-2 gap-6">
        <Card v-for="card in filteredCardList" :key="card.id" v-bind="card" />
      </div>
      <div v-if="targetDisplayType === 'row'" class="col-span-9 mt-6 lg:mt-0 space-y-4">
        <RowCard v-for="card in filteredCardList" :key="card.id" v-bind="card" v-bind:disableDeleteButton="true"
          v-bind:showAvailability="false" v-bind:showRating="true" v-bind:showRemoveFromWishlist="true" />
      </div>
      <!-- product wrapper end -->
      <div class="flex items-center justify-between border-t border-gray-200 bg-white px-4 py-3 sm:px-6">
        <div class="flex flex-1 justify-between sm:hidden">
          <a href="#"
            class="relative inline-flex items-center rounded-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50">Previous</a>
          <a href="#"
            class="relative ml-3 inline-flex items-center rounded-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50">Next</a>
        </div>
      </div>
      <!-- Pagination -->
      <div class="hidden sm:flex sm:flex-1 sm:items-center sm:justify-between">
        <div>
          <p class="text-sm text-gray-700">
            Showing
            <span class="font-medium">1</span>
            to
            <span class="font-medium">10</span>
            of
            <span class="font-medium">{{ cardList.length }}</span>
            results
          </p>
        </div>
        <div>
          <nav class="isolate inline-flex -space-x-px rounded-md shadow-sm" aria-label="Pagination">
            <a href="#"
              class="relative inline-flex items-center rounded-l-md px-2 py-2 text-gray-400 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
              <span class="sr-only">Previous</span>
              <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                <path fill-rule="evenodd"
                  d="M12.79 5.23a.75.75 0 01-.02 1.06L8.832 10l3.938 3.71a.75.75 0 11-1.04 1.08l-4.5-4.25a.75.75 0 010-1.08l4.5-4.25a.75.75 0 011.06.02z"
                  clip-rule="evenodd" />
              </svg>
            </a>
            <!-- Current: "z-10 bg-indigo-600 text-white focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600", Default: "text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:outline-offset-0" -->
            <a href="#" aria-current="page"
              class="relative z-10 inline-flex items-center bg-primary px-4 py-2 text-sm font-semibold text-white focus:z-20 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">1</a>
            <a href="#"
              class="relative inline-flex items-center px-4 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">2</a>
            <a href="#"
              class="relative hidden items-center px-4 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0 md:inline-flex">3</a>
            <span
              class="relative inline-flex items-center px-4 py-2 text-sm font-semibold text-gray-700 ring-1 ring-inset ring-gray-300 focus:outline-offset-0">...</span>
            <a href="#"
              class="relative hidden items-center px-4 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0 md:inline-flex">8</a>
            <a href="#"
              class="relative inline-flex items-center px-4 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">9</a>
            <a href="#"
              class="relative inline-flex items-center px-4 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">10</a>
            <a href="#"
              class="relative inline-flex items-center rounded-r-md px-2 py-2 text-gray-400 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus:z-20 focus:outline-offset-0">
              <span class="sr-only">Next</span>
              <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                <path fill-rule="evenodd"
                  d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z"
                  clip-rule="evenodd" />
              </svg>
            </a>
          </nav>
        </div>
      </div>
      <!-- Pagination -->
    </div>
    <!-- products end -->
  </div>
  <!-- shop wrapper end -->
</template>

<script setup lang="ts">
import Card from '@/components/Card.vue'
import RowCard from '@/components/RowCard.vue'
import { onMounted, computed, ref, watch } from 'vue'
import ProductAPI from '@/api/product.api'
import CategoryProps from '@/interfaces/category'
import CardProps from '@/interfaces/card'

const cardList = ref<CardProps[]>([])
const categoryList = ref<CategoryProps[]>([])
const filteredCardList = ref<CardProps[]>([])
const minPrice = ref('')
const maxPrice = ref('')

type DisplayTypes = 'col' | 'row'
const targetDisplayType = ref<DisplayTypes>('col')

const handleChangeDisplayType = (type: DisplayTypes) => {
  targetDisplayType.value = type
}

const filterByCategory = (categoryId: number) => {
  filteredCardList.value = cardList.value.filter(card => card.category_id.id === categoryId)
}
const filterByPrice = () => {
  const min = parseFloat(minPrice.value) || 0
  const max = parseFloat(maxPrice.value) || Infinity
  filteredCardList.value = cardList.value.filter(card => card.price >= min && card.price <= max)
}
const sortProducts = (event: Event) => {
  const value = (event.target as HTMLSelectElement).value
  if (value === 'low-high') {
    filteredCardList.value.sort((a, b) => a.price - b.price)
  } else if (value === 'high-low') {
    filteredCardList.value.sort((a, b) => b.price - a.price)
  } else if (value === 'latest') {
    filteredCardList.value.sort((a, b) => new Date(b.created_at).getTime() - new Date(a.created_at).getTime())
  } else {
    filteredCardList.value = cardList.value // Default sorting
  }
}

const showAllProducts = () => {
  filteredCardList.value = cardList.value; // Hiển thị tất cả sản phẩm
}

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
