<script setup>
import img1 from './assets/card-img-1.png'
import img2 from './assets/card-img-2.png'
import img3 from './assets/card-img-3.png'
import img4 from './assets/card-img-4.png'
import img5 from './assets/card-img-5.png'
import img6 from './assets/card-img-6.png'
import img7 from './assets/card-img-7.png'
import img8 from './assets/card-img-8.png'
import img9 from './assets/card-img-9.png'
</script>



<template>
  <div class="h-screen flex flex-col md:flex-row overflow-hidden bg-gray-100">
    <!-- Mobile Topbar START-->
    <header class="bg-white shadow p-4 flex justify-between items-center md:hidden">
      <button @click="toggleSidebar" class="text-2xl">☰</button>
      <h1 class="text-lg font-semibold">Chairsade</h1>
      <div><img src="https://randomuser.me/api/portraits/men/75.jpg"  alt="Robert Lindley"  class="w-10 h-10 rounded-full"/></div>
    </header>

    <!-- Overlay for mobile sidebar -->
    <div v-if="sidebarOpen" class="fixed inset-0 bg-black bg-opacity-50 z-40 md:hidden" @click="toggleSidebar"></div>

    <!-- Left Sidebar START-->
    <aside
      :class="[
        'fixed main-left-panel z-50 inset-y-0 left-0 w-64 bg-white shadow transform transition-transform duration-300 flex flex-col justify-between md:relative md:translate-x-0',
        sidebarOpen ? 'translate-x-0' : '-translate-x-full',
      ]"
    >
      <div>
        <div class="p-6 text-lg font-bold border-b-[0.1px] border-gray-300 text-white">CHAIRSADE</div>
        <nav class="main-nav-bar p-4 space-y-2 ">
          <a href="#" class="main-nav-bar__item flex items-center py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500">
            <i class="fa-solid fa-house mr-2"></i> Home</a>
          <!-- Dropdown Menu START -->
          <div>
            <button
              class="w-full text-left py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500 flex justify-between items-center"
              @click="toggleDropdown('settings')"> <div class="flex items-center">
                <i class="fas fa-stopwatch mr-2"></i> View Sessions </div>
              <span :class="{ 'rotate-180': dropdowns.settings }" class="transition-transform"><span class="text-xs"><i class="fa-solid fa-caret-down"></i></span></span>
            </button>
            <div v-if="dropdowns.settings" class="pl-6">
              <a href="#" class="flex items-center py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500"><i class="fa-solid fa-plus mr-2"></i>Session - 1</a>
              <a href="#" class="flex items-center py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500"><i class="fa-solid fa-plus mr-2"></i>Session - 2</a>
            </div>
          </div>
          <!-- Dropdown Menu END -->
           <a href="#" class="main-nav-bar__item flex items-baseline py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500">
           <i class="fa-solid fa-circle-user mr-2"></i>Patient Records</a>
           <a href="#" class="main-nav-bar__item flex items-center py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500">
            <i class="fa-regular fa-image mr-2"></i> Media</a>
           <a href="#" class="main-nav-bar__item flex items-center py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500">
            <i class="fa-solid fa-desktop mr-2"></i> Virtual Consultation</a>
           <a href="#" class="main-nav-bar__item flex items-center py-2 px-4 rounded-[8px] hover:bg-white/15 text-white hover:text-green-500">
           <i class="fa-solid fa-chart-simple mr-2"></i> Statistics </a>
        </nav>
      </div>

      <!-- Profile bottom START -->
      <div class="border-t-[0.1px] border-gray-300 p-4 relative main-nav-profile">
        <button
          @click="toggleUserMenu"
          class="w-full flex items-center justify-between hover:bg-white/15 rounded px-3 py-2 hover:text-green-500 cursor-pointer"
        >
          <div class="flex items-center space-x-2">
            <img
              src="https://ui-avatars.com/api/?name=Robert+Lindley&background=fff&color=000"
              alt="User"
              class="w-8 h-8 rounded-full"
            />
            <div class=" main-nav-profile__details"> 
              <div class="text-sm font-medium text-left text-white main-nav-profile__name">John Doe</div>
              <div class="text-xs w-36 truncate main-nav-profile__email">robertlindley@shoreditchdesign.com</div>
            </div>
          </div>
          <span :class="{ 'rotate-180': userMenuOpen }" class="transition-transform text-xs"><i class="fa-solid fa-caret-down"></i></span>
        </button>

        <div
          v-if="userMenuOpen"
          class="absolute bottom-16 left-4 right-4 bg-green-800 shadow-md rounded p-2 space-y-1 z-50">
          <a href="#" class="flex items-center  px-4 py-2 text-sm rounded-[8px] text-white hover:bg-black/15  hover:text-green-500"><i class="fa-solid fa-user-tie mr-2"></i>Profile</a>
          <a href="#" class="flex items-center  px-4 py-2 text-sm rounded-[8px] text-white hover:bg-black/15  hover:text-green-500"><i class="fa-solid fa-gear mr-2"></i>Settings</a>
          <a href="#" class="flex items-center  px-4 py-2 text-sm rounded-[8px] text-white hover:bg-black/15  hover:text-green-500"><i class="fa-solid fa-right-from-bracket mr-2"></i>Logout</a>
        </div>
      </div>
      <!-- Profile bottom END -->
    </aside>

    <!-- Main content Right sidebar START -->
    <div class="flex-1 flex flex-col md:flex-row overflow-hidden relative main-expand-container">
      <!-- Main content -->
      <div class="flex-1 flex flex-col main-expand-container__inner">
        <!-- Desktop Topbar START-->
        <header class="hidden md:flex bg-white border-b-[0.1px] border-gray-300 px-4 py-2 justify-between items-center">
          <!-- Left side: Breadcrumb + Title -->
          <div>
            <nav class="text-sm text-gray-500 space-x-1 mb-1 select-none">
              <span class="hover:underline cursor-pointer">Patient records</span>
              <span class="px-2"><i class="fa-solid fa-angle-right"></i></span>
              <span class="hover:underline cursor-pointer">Robert lindley</span>
              <span class="px-2"><i class="fa-solid fa-angle-right"></i></span>
              <span class="text-gray-800 font-medium">Emergency visit for tooth ache</span>
            </nav>            
          </div>

          <!-- Right side Sidebar Toggle START-->
          <div class="flex items-center gap-4">
            <span><img src="https://randomuser.me/api/portraits/men/75.jpg"  alt="Robert Lindley"  class="w-6 h-6 rounded-full"/></span>
            <button
              @click="toggleRightSidebar"
              class="text-gray-600 hover:text-black transition-transform duration-300 w-8 h-8 rounded-full bg-green-500/20 hover:bg-green-800/25 transform"
              :class="{ 'rotate-180': !rightSidebarOpen }"
              title="Toggle Sidebar"
            >
              <span class="text-xl inline-block transform transition-transform text-black "><i class="fa-solid fa-xs fa-angles-right cursor-pointer"></i></span>
            </button>
          </div>
          <!-- Right side Sidebar Toggle END-->
        </header>
        <!-- Desktop Topbar END-->


      <!-- Tabs section START -->
      <div class="flex items-center justify-between mb-4 bg-white border-b-[0.5px] border-gray-300 px-4 py-0 ">
        <!-- Tabs -->
        <nav class="flex space-x-8" aria-label="Tabs">
          <a href="#" class="py-4 px-1 border-b-2 font-medium text-lg border-green-500 text-green-600">
            Notes
          </a>
          <a href="#" class="py-4 px-1 border-b-2 font-medium text-lg border-transparent text-gray-500 hover:text-green-600 hover:border-green-500">
            Bundles
          </a>
        </nav>

        
        <button class="text-sm font-semibold text-white bg-green-600 hover:bg-green-700 px-2 md:px-4 py-2  rounded-md cursor-pointer">
          <i class="fa-solid fa-pen mr-2"></i> Edit Session
        </button>
      </div>
       <!-- Tabs section END --> 

        <!-- Main grid START -->
       <main class="flex-1 overflow-y-auto p-4 main-container-center">
          <div class="bg-white p-8 rounded shadow">
              <!-- Header -->
              <div class="flex items-center justify-between mb-4">
                <button class="px-4 py-1 text-sm font-medium border-[0.5px] border-gray-300 hover:bg-green-500/10 rounded-[8px] cursor-pointer">
                  <i class="fa-solid fa-file mr-2"></i> Template A
                </button>
                <div class="space-x-2">
                  <button class="py-1 px-2 text-gray-500 hover:text-gray-700 border-[0.5px] border-gray-300 rounded-[8px] cursor-pointer"><i class="fas fa-copy"></i></button>
                  <button class="py-1 px-2 text-gray-500 hover:text-gray-700 border-[0.5px] border-gray-300 rounded-[8px] cursor-pointer"><i class="fa-solid fa-circle-down"></i></button>
                </div>
              </div>

              <!-- Notes Title -->
              <h2 class="text-3xl font-semibold">Notes</h2>
              <p class="text-sm text-gray-400 mb-4">Last updated today 09:15 AM</p>
              <hr class="mb-6 text-gray-300" />

              <!-- Form Fields -->
              <div class="space-y-4">
                <div>
                  <p class="font-medium">Dentist</p>
                  <p>Dr John Smith</p>
                </div>

                <div>
                  <p class="font-medium">Nurse</p>
                  <input type="text" placeholder="Type here"
                        class="mt-1 w-56 max-w-full px-3 py-2 border-0 border-b-2 border-b-cyan-500/30 focus:outline-none focus:border-b-orange-500" />
                </div>

                <div>
                  <p class="font-medium">When did the fracture occur?</p>
                  <div class="mt-2 flex flex-wrap gap-2">
                    <button class="px-3 py-1 border border-gray-300 rounded-[4px] text-sm hover:text-green-600 hover:bg-green-50 hover:border-green-50 cursor-pointer">Today</button>
                    <button class="px-3 py-1 bg-green-50 text-green-600 border-gray-300 rounded-[4px] text-sm hover:text-green-600 hover:bg-green-50 hover:border-green-50 cursor-pointer">Yesterday</button>
                    <button class="px-3 py-1 border border-gray-300 rounded-[4px] text-sm hover:text-green-600 hover:bg-green-50 hover:border-green-50 cursor-pointer">Several days ago</button>
                    <button class="px-3 py-1 border border-gray-300 rounded-[4px] text-sm hover:text-green-600 hover:bg-green-50 hover:border-green-50 cursor-pointer">Over a week ago</button>
                    <button class="px-3 py-1 border border-gray-300 rounded-[4px] text-sm hover:text-green-600 hover:bg-green-50 hover:border-green-50 cursor-pointer">N/A</button>
                  </div>
                </div>

                <div>
                  <p class="font-medium flex items-center">
                    Location of broken tooth
                    <span class="ml-2 text-gray-400 cursor-pointer" title="More info">
                      <i class="fas fa-info-circle text-blue-400"></i>                      
                    </span>
                  </p>
                  <input type="text" value="Broken tooth lorem"
                        class="mt-1 w-56 max-w-full pr-3 py-2 border-0 border-b-2 border-b-cyan-500/30 focus:outline-none focus:border-b-orange-500" />
                </div>

                <div>
                  <p class="font-medium flex items-center">Reason for attendance</p>
                  <input type="text" value="Broken tooth lorem"
                        class="mt-1 w-56 max-w-full pr-3 py-2 border-0 border-b-2 border-b-cyan-500/30 focus:outline-none focus:border-b-orange-500" />
                </div>

                <div>
                  <p class="font-medium">When did the fracture occur?</p>
                  <input type="text" value="Broken tooth"
                        class="mt-1 w-56 max-w-full pr-3 py-2 border-0 border-b-2 border-b-cyan-500/30 focus:outline-none focus:border-b-orange-500" />
                </div>

                <div>
                  <p class="font-medium">How did it happen?</p>
                  <input type="text" value="Broken tooth"
                        class="mt-1 w-56 max-w-full pr-3 py-2 border-0 border-b-2 border-b-cyan-500/30 focus:outline-none focus:border-b-orange-500" />
                </div>
              </div>

                    
          </div>
       </main>
       <!-- Main grid END -->
      </div>

      <!-- Right Sidebar START -->
      <transition name="slide">
        <aside
          v-if="rightSidebarOpen"
          class="w-full md:w-100 bg-white shadow-md border-t md:border-t-0 space-y-4 absolute md:relative right-0 h-full z-20 flex flex-col">
           <div class="flex justify-center py-6 border-b-[0.1px] border-gray-300">
           <h2 class="text-neutral-900 font-bold text-xl">Timeline</h2>
           </div>
      <!-- Right Sidebar END -->

      <!-- Right Sidebar Top Widget START-->
      <div class="overflow-y-auto px-4 space-y-4 flex-1 right-sidebar-container">
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">          
            <img :src="img1" alt="card-img-1" />
          </div>          
          <div>
            <p class="text-xs text-gray-500">09:45 AM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer">Consent form</span> signed</p>
          </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
            <img :src="img2" alt="card-img-2" />
          </div>
          <div>
            <p class="text-xs text-gray-500">09:45 AM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer"></span>3 treatments chosen</p>
            <ul class="text-sm text-gray-600">
              <li>Root canal</li>
              <li>Dental extraction</li>
              <li>Teeth whitening</li>
            </ul>
          </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
            <img :src="img3" alt="card-img-3" />
          </div>
          <div>
          <p class="text-xs text-gray-500">3 July, 16:15 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer">Bundle 2</span> sent</p>
            <ul class="text-sm text-gray-600">
              <li>Johnsmith@gmail.com</li>
            </ul>
          </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
             <img :src="img4" alt="card-img-4" />
            </div>
            <div>
            <p class="text-xs text-gray-500">3 July, 12:54 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer">Consent form</span> declined</p>
            <ul class="text-sm text-gray-600">
              <li></li>
            </ul>
            </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
            <img :src="img5" alt="card-img-5" />
          </div>
          <div>
            <p class="text-xs text-gray-500">3 July, 12:54 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer">Bundle 1</span> viewed</p>
            <ul class="text-sm text-gray-600">
              <li></li>
            </ul>
          </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
            <img :src="img3" alt="card-img-6" />
          </div>
          <div>
            <p class="text-xs text-gray-500">1 July, 10:05 AM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer">Bundle 1</span> sent</p>
            <ul class="text-sm text-gray-600">
              <li>ohnsmith@gmail.com</li>
            </ul>
          </div>
        </div>

        <div class="border-t-3 border-dotted border-gray-300 w-full mt-5"></div>
        <p class="text-sm text-gray-500 pb-0">Appointment ends • 1 July, 10:00 AM</p>

        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class=" rounded-md">
            <img :src="img6" alt="card-img-6" />
            </div>
            <div>
            <p class="text-xs text-gray-500">9:45 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer"></span> Annotation added</p>
            <ul class="text-sm text-gray-600">
              <li></li>
            </ul>
            </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
            <img :src="img7" alt="card-img-7" />
          </div>
          <div>
            <p class="text-xs text-gray-500">9:45 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer">Periodontitis selected</span> played </p>
            <ul class="text-sm text-gray-600">
              <li>70% complete</li>
            </ul>
          </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
           <img :src="img8" alt="card-img-8" />
          </div>
          <div>
            <p class="text-xs text-gray-500">9:45 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer"></span> Periodontis video</p>
            <ul class="text-sm text-gray-600">
              <li></li>
            </ul>
          </div>
        </div>
        <div class="flex items-start p-4 gap-3 bg-white rounded-lg shadow-sm max-w-sm w-full hover:bg-green-500/10 cursor-pointer">
          <div class="rounded-md">
           <img :src="img9" alt="card-img-9" />
          </div>
          <div>
            <p class="text-xs text-gray-500">9:45 PM</p>
            <p class="text-sm"><span class="underline font-medium cursor-pointer"></span> Periodontitis mentioned</p>
            <ul class="text-sm text-gray-600">
              <li></li>
            </ul>
          </div>
        </div>

        <p class="text-sm text-gray-500 pb-8">Appointment begins • 1 July, 09:45 AM</p>
      </div>
      <!-- Right Sidebar Top Widget END-->


        </aside>
      </transition>
      <!-- Right Sidebar END -->
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



</style>