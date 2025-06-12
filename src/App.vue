<template>
  <div class="h-screen flex flex-col md:flex-row overflow-hidden bg-gray-100">
    <!-- Mobile Topbar -->
    <header class="bg-white shadow p-4 flex justify-between items-center md:hidden">
      <button @click="toggleSidebar" class="text-2xl">☰</button>
      <h1 class="text-lg font-semibold">Dashboard</h1>
      <div>👤</div>
    </header>

    <!-- Overlay for mobile sidebar -->
    <div v-if="sidebarOpen" class="fixed inset-0 bg-black bg-opacity-50 z-40 md:hidden" @click="toggleSidebar"></div>

    <!-- Left Sidebar -->
    <aside
      :class="[
        'fixed z-50 inset-y-0 left-0 w-64 bg-white shadow transform transition-transform duration-300 flex flex-col justify-between md:relative md:translate-x-0',
        sidebarOpen ? 'translate-x-0' : '-translate-x-full',
      ]"
    >
      <div>
        <div class="p-6 text-lg font-bold border-b">My Dashboard</div>
        <nav class="p-4 space-y-2">
          <a href="#" class="flex items-center py-2 px-4 rounded hover:bg-gray-200">
            <svg
              class="w-5 h-5 mr-2 text-gray-600"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              viewBox="0 0 24 24"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M3 12l2-2 4 4 8-8 4 4"></path>
            </svg>
            Dashboard
          </a>

          <!-- Dropdown Menu -->
          <div>
            <button
              class="w-full text-left py-2 px-4 rounded hover:bg-gray-200 flex justify-between items-center"
              @click="toggleDropdown('reports')"
            >
              <div class="flex items-center">
                <svg
                  class="w-5 h-5 mr-2 text-gray-600"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path d="M9 17v-6a2 2 0 0 1 4 0v6"></path>
                  <path d="M12 15h.01"></path>
                  <path d="M4 17h16"></path>
                </svg>
                Reports
              </div>
              <span :class="{ 'rotate-180': dropdowns.reports }" class="transition-transform">▼</span>
            </button>
            <div v-if="dropdowns.reports" class="pl-6">
              <a href="#" class="block py-1 px-2 rounded hover:bg-gray-100">Sales</a>
              <a href="#" class="block py-1 px-2 rounded hover:bg-gray-100">Analytics</a>
            </div>
          </div>

          <div>
            <button
              class="w-full text-left py-2 px-4 rounded hover:bg-gray-200 flex justify-between items-center"
              @click="toggleDropdown('settings')"
            >
              <div class="flex items-center">
                <svg
                  class="w-5 h-5 mr-2 text-gray-600"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <circle cx="12" cy="12" r="3"></circle>
                  <path
                    d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33
                       1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09a1.65 1.65 0 0 0-1-1.51
                       1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82
                       1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09a1.65 1.65 0 0 0 1.51-1
                       1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06a1.65 1.65 0 0 0 1.82.33h.09
                       a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51h.09
                       a1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06
                       a1.65 1.65 0 0 0-.33 1.82v.09a1.65 1.65 0 0 0 1.51 1H21
                       a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"
                  ></path>
                </svg>
                Settings
              </div>
              <span :class="{ 'rotate-180': dropdowns.settings }" class="transition-transform">▼</span>
            </button>
            <div v-if="dropdowns.settings" class="pl-6">
              <a href="#" class="block py-1 px-2 rounded hover:bg-gray-100">Account</a>
              <a href="#" class="block py-1 px-2 rounded hover:bg-gray-100">Preferences</a>
            </div>
          </div>
        </nav>
      </div>

      <!-- Profile at bottom -->
      <div class="border-t p-4 relative">
        <button
          @click="toggleUserMenu"
          class="w-full flex items-center justify-between hover:bg-gray-100 rounded px-3 py-2"
        >
          <div class="flex items-center space-x-2">
            <img
              src="https://via.placeholder.com/32"
              alt="User"
              class="w-8 h-8 rounded-full"
            />
            <div>
              <div class="text-sm font-medium">John Doe</div>
              <div class="text-xs text-gray-500">Admin</div>
            </div>
          </div>
          <span :class="{ 'rotate-180': userMenuOpen }" class="transition-transform">▼</span>
        </button>

        <div
          v-if="userMenuOpen"
          class="absolute bottom-16 left-4 right-4 bg-white shadow-md rounded p-2 space-y-1 z-50"
        >
          <a href="#" class="block px-4 py-2 text-sm hover:bg-gray-100">Profile</a>
          <a href="#" class="block px-4 py-2 text-sm hover:bg-gray-100">Settings</a>
          <a href="#" class="block px-4 py-2 text-sm hover:bg-gray-100">Logout</a>
        </div>
      </div>
    </aside>

    <!-- Main content + Right sidebar -->
    <div class="flex-1 flex flex-col md:flex-row overflow-hidden relative">
      <!-- Main content -->
      <div class="flex-1 flex flex-col">
        <!-- Desktop Topbar -->
        <header class="hidden md:flex bg-white shadow p-4 justify-between items-center">
          <!-- Left side: Breadcrumb + Title -->
          <div>
            <nav class="text-sm text-gray-500 space-x-1 mb-1 select-none">
              <span class="hover:underline cursor-pointer">Home</span>
              <span>/</span>
              <span class="hover:underline cursor-pointer">Dashboard</span>
              <span>/</span>
              <span class="text-gray-800 font-medium">Reports</span>
            </nav>
            <h1 class="text-xl font-semibold">Dashboard</h1>
          </div>

          <!-- Right side: User + Right Sidebar Toggle -->
          <div class="flex items-center gap-4">
            <span>👤 User</span>
            <button
              @click="toggleRightSidebar"
              class="text-gray-600 hover:text-black transition-transform duration-300"
              :class="{ 'rotate-180': !rightSidebarOpen }"
              title="Toggle Sidebar"
            >
              <span class="text-xl inline-block transform transition-transform">⇨</span>
            </button>
          </div>
        </header>

        <!-- Main grid -->
       <main class="flex-1 overflow-y-auto p-4">
  <div class="bg-white p-4 rounded shadow">📊 Main Card 1</div>
</main>
      </div>

      <!-- Right Sidebar -->
      <transition name="slide">
        <aside
          v-if="rightSidebarOpen"
          class="w-full md:w-72 bg-white shadow-md border-t md:border-t-0 md:border-l p-4 space-y-4 absolute md:relative right-0 h-full z-20"
        >
          <div class="bg-gray-100 p-4 rounded shadow">
            <h2 class="text-md font-semibold mb-2">📅 Calendar Widget</h2>
            <p>Upcoming events or mini calendar view here.</p>
          </div>
          <div class="bg-gray-100 p-4 rounded shadow">
            <h2 class="text-md font-semibold mb-2">💬 Messages Widget</h2>
            <p>Recent messages, notifications, or chat preview.</p>
          </div>
        </aside>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      sidebarOpen: false,
      rightSidebarOpen: true,
      userMenuOpen: false,
      dropdowns: {
        reports: false,
        settings: false,
      },
    };
  },
  methods: {
    toggleSidebar() {
      this.sidebarOpen = !this.sidebarOpen;
    },
    toggleRightSidebar() {
      this.rightSidebarOpen = !this.rightSidebarOpen;
    },
    toggleDropdown(section) {
      this.dropdowns[section] = !this.dropdowns[section];
    },
    toggleUserMenu() {
      this.userMenuOpen = !this.userMenuOpen;
    },
  },
};
</script>

<style scoped>
/* Right sidebar slide animation */
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease, opacity 0.3s ease;
}
.slide-enter-from,
.slide-leave-to {
  transform: translateX(100%);
  opacity: 0;
}
</style>