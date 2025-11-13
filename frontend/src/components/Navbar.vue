<template>
  <nav class="bg-gray-900 shadow-lg">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex">
          <div class="flex-shrink-0 flex items-center">
            <h1 class="text-2xl font-bold text-white">Task Manager</h1>
          </div>
          <div class="hidden sm:ml-6 sm:flex sm:space-x-8">
            <router-link
              to="/"
              class="border-transparent text-gray-300 hover:border-gray-400 hover:text-white inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium"
              active-class="border-white text-white"
            >
              Dashboard
            </router-link>
            <router-link
              to="/tasks"
              class="border-transparent text-gray-300 hover:border-gray-400 hover:text-white inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium"
              active-class="border-white text-white"
            >
              Tareas
            </router-link>
          </div>
        </div>
        <div class="flex items-center">
          <!-- Mobile menu button -->
          <div class="sm:hidden">
            <button
              @click="toggleMobileMenu"
              class="text-gray-300 hover:text-white focus:outline-none focus:text-white"
            >
              <svg class="h-6 w-6 fill-current" viewBox="0 0 24 24">
                <path v-if="!isMobileMenuOpen" fill-rule="evenodd" d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"/>
                <path v-else fill-rule="evenodd" d="M18.278 16.864a1 1 0 0 1-1.414 1.414l-4.829-4.828-4.828 4.828a1 1 0 0 1-1.414-1.414l4.828-4.829-4.828-4.828a1 1 0 0 1 1.414-1.414l4.829 4.828 4.828-4.828a1 1 0 0 1 1.414 1.414l-4.828 4.829 4.828 4.828z"/>
              </svg>
            </button>
          </div>
          <div class="hidden sm:block ml-3 relative">
            <div class="flex items-center space-x-4">
              <span class="text-sm text-gray-300">{{ authStore.user?.name }}</span>
              <button
                @click="handleLogout"
                class="bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded text-sm font-medium transition cursor-pointer"
              >
                Cerrar Sesión
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Mobile menu -->
    <div v-if="isMobileMenuOpen" class="sm:hidden">
      <div class="px-2 pt-2 pb-3 space-y-1 bg-gray-800">
        <router-link
          to="/"
          @click="closeMobileMenu"
          class="block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700"
          active-class="text-white bg-gray-700"
        >
          Dashboard
        </router-link>
        <router-link
          to="/tasks"
          @click="closeMobileMenu"
          class="block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700"
          active-class="text-white bg-gray-700"
        >
          Tareas
        </router-link>
        <div class="border-t border-gray-700 pt-4 pb-3">
          <div class="flex items-center px-5">
            <div class="text-base font-medium text-white">{{ authStore.user?.name }}</div>
          </div>
          <div class="mt-3 px-2">
            <button
              @click="handleLogout"
              class="block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700 w-full text-left"
            >
              Cerrar Sesión
            </button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue'
import { useAuthStore } from '@/stores/auth'
import { useRouter } from 'vue-router'

const authStore = useAuthStore()
const router = useRouter()

const isMobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}

const handleLogout = async () => {
  await authStore.logout()
  router.push('/login')
  closeMobileMenu()
}
</script>
