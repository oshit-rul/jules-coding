<template>
  <div class="container mx-auto">
    <!-- Main Content Area with Sidebar -->
    <div class="flex flex-col md:flex-row gap-8 mt-8">
      <!-- Category Sidebar (Left Side) -->
      <div class="w-full md:w-1/4">
        <CategorySidebar />
      </div>

      <!-- Main Content (Right Side) -->
      <div class="w-full md:w-3/4">
        <!-- Hero Slider -->
        <HeroSlider class="mb-12" />

        <!-- Featured Categories Section -->
        <section class="mb-12">
          <h2 class="text-3xl font-bold text-gray-800 mb-6">Featured Categories</h2>
          <div v-if="featuredCategories.length" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
            <div v-for="category in featuredCategories" :key="category.id"
                 class="bg-white p-6 rounded-lg shadow-lg hover:shadow-xl transition-shadow">
              <NuxtLink :to="`/categories/${category.slug}`" class="block">
                <h3 class="text-xl font-semibold text-blue-700 hover:text-blue-900">{{ category.name }}</h3>
                <p class="text-gray-600 mt-2">Explore products in {{ category.name }}</p>
              </NuxtLink>
            </div>
          </div>
          <p v-else class="text-gray-500">Loading featured categories...</p>
        </section>

        <!-- Best Sellers Section -->
        <section class="mb-12">
          <h2 class="text-3xl font-bold text-gray-800 mb-6">Best Sellers</h2>
          <div v-if="bestSellingProducts.length" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <ProductCard v-for="product in bestSellingProducts" :key="product.id" :product="product" />
          </div>
          <p v-else class="text-gray-500">Loading best sellers...</p>
        </section>

        <!-- Category-wise Products (Example: Electronics) -->
        <section class="mb-12" v-if="electronicsProducts.length">
          <h2 class="text-3xl font-bold text-gray-800 mb-6">Electronics</h2>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <ProductCard v-for="product in electronicsProducts" :key="product.id" :product="product" />
          </div>
        </section>

        <!-- Category-wise Products (Example: Clothing) -->
        <section class="mb-12" v-if="clothingProducts.length">
          <h2 class="text-3xl font-bold text-gray-800 mb-6">Clothing</h2>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <ProductCard v-for="product in clothingProducts" :key="product.id" :product="product" />
          </div>
        </section>

        <!-- Brands Section -->
        <section class="mb-12">
          <h2 class="text-3xl font-bold text-gray-800 mb-6">Our Brands</h2>
          <div v-if="brands.length" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 items-center">
            <BrandLogo v-for="brand in brands" :key="brand.id" :brand="brand" />
          </div>
          <p v-else class="text-gray-500">Loading brands...</p>
        </section>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import CategorySidebar from '~/components/CategorySidebar.vue';
import HeroSlider from '~/components/HeroSlider.vue';
import ProductCard from '~/components/ProductCard.vue';
import BrandLogo from '~/components/BrandLogo.vue';

// Data refs
const allProducts = ref([]);
const allCategories = ref([]);
const featuredCategories = ref([]);
const bestSellingProducts = ref([]);
const electronicsProducts = ref([]);
const clothingProducts = ref([]);
const brands = ref([]);

// Fetch all necessary data on mount
onMounted(async () => {
  try {
    // Fetch products
    const productResponse = await fetch('/storage/products.json');
    if (!productResponse.ok) throw new Error('Failed to fetch products');
    const productsData = await productResponse.json();
    allProducts.value = productsData;

    // Filter products
    bestSellingProducts.value = productsData.filter(p => p.best_seller).slice(0, 4); // Show top 4 best sellers
    electronicsProducts.value = productsData.filter(p => p.category_slug === 'electronics').slice(0, 4);
    clothingProducts.value = productsData.filter(p => p.category_slug === 'clothing').slice(0, 4);


    // Fetch categories
    const categoriesResponse = await fetch('/storage/categories.json');
    if (!categoriesResponse.ok) throw new Error('Failed to fetch categories');
    const categoriesData = await categoriesResponse.json();
    allCategories.value = categoriesData;
    // Assuming first 2-3 categories are "featured" for this example
    featuredCategories.value = categoriesData.slice(0, 3);


    // Fetch brands
    const brandsResponse = await fetch('/storage/brands.json');
    if (!brandsResponse.ok) throw new Error('Failed to fetch brands');
    brands.value = await brandsResponse.json();

  } catch (error) {
    console.error("Error fetching homepage data:", error);
    // Handle errors appropriately
  }
});
</script>

<style scoped>
/* Scoped styles for the home page if needed */
.container {
  /* Ensure container is not overly wide if global one is too large, or rely on global */
}
</style>
