<!-- This example requires Tailwind CSS v2.0+ -->
<template>
  <!-- This example requires Tailwind CSS v2.0+ -->
  <nav class="bg-white font-nunito">
    <div class="mx-auto px-2 sm:px-6 lg:px-8">
      <div class="relative flex items-center justify-between h-16">
        <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
          <!-- Mobile menu button-->
          <button
            type="button"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
            aria-controls="mobile-menu"
            @click="toggleMobileNavBar()"
          >
            <span class="sr-only">Open main menu</span>
            <!--
            Icon when menu is closed.

            Heroicon name: outline/menu

            Menu open: "hidden", Menu closed: "block"
          -->
            <svg
              class="block h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
            </svg>
            <!--
            Icon when menu is open.

            Heroicon name: outline/x

            Menu open: "block", Menu closed: "hidden"
          -->
            <svg
              class="hidden h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <div class="flex-1 flex items-center justify-center sm:justify-between">
          <div class="flex-shrink-0 flex items-center">
            <nuxt-img
              src="/img/ben_bighead.png"
              width="50"
              height="50"
              class="mr-1"
              alt="benjamin looi logo"
            />
            <h1 class="color-coolGray text-lg">Benjamin Looi</h1>
          </div>
          <div class="hidden sm:block sm:ml-6">
            <div class="flex space-x-4">
              <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
              <NuxtLink
                to="/"
                exact
                class="text-gray-400 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-semibold"
              >
                Home
              </NuxtLink>

              <NuxtLink
                to="/projects"
                exact
                class="text-gray-400 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-semibold"
              >
                Projects
              </NuxtLink>

              <a
                href="https://resume.benjaminlooi.dev"
                class="text-gray-400 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-semibold"
              >
                Resume
              </a>

              <a
                href="https://blog.benjaminlooi.dev"
                class="text-gray-400 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-semibold"
              >
                Blog
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Mobile menu, show/hide based on menu state. -->
    <div id="mobile-menu" ref="mobileMenu" class="sm:hidden">
      <div class="px-2 pt-2 pb-3 space-y-1">
        <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
        <NuxtLink
          to="/"
          exact
          class="text-gray-400 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-semibold"
          @click.native="closeMobileMenu()"
        >
          Home
        </NuxtLink>

        <NuxtLink
          to="/projects"
          exact
          class="text-gray-400 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-semibold"
          @click.native="closeMobileMenu()"
        >
          Projects
        </NuxtLink>

        <a
          href="https://resume.benjaminlooi.dev"
          class="text-gray-400 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-semibold"
          @click.native="closeMobileMenu()"
        >
          Resume
        </a>

        <a
          href="https://blog.benjaminlooi.dev"
          class="text-gray-400 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-semibold"
        >
          Blog
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data: () => ({
    tl: null,
    mobileMenuRef: null,
    mobileNavBarIsActive: false,
  }),
  mounted() {
    this.tl = this.$gsap.timeline({ paused: true })
    this.mobileMenuRef = this.$refs.mobileMenu
    this.tl
      .addLabel('start')
      .fromTo(
        this.mobileMenuRef,
        {
          opacity: 0,
          height: 0,
        },
        {
          opacity: 1,
          height: 'auto',
          duration: 0.2,
          ease: 'power2.inOut',
        }
      )
      .addLabel('end')
  },
  methods: {
    logCurrentLabel() {
      // console.log(this.tl.currentLabel())
    },
    toggleMobileNavBar() {
      if (!this.mobileNavBarIsActive) {
        this.mobileNavBarIsActive = true
        this.tl.play()
      } else {
        this.mobileNavBarIsActive = false
        this.tl.reverse()
      }
    },
    closeMobileMenu() {
      this.mobileNavBarIsActive = false
      this.tl.reverse()
    },
  },
}
</script>

<style lang="scss" scoped>
a.nuxt-link-exact-active {
  color: rgba(31, 41, 55, var(--tw-text-opacity));
  font-weight: bold;

  &:hover {
    color: #fff;
  }
}

#mobile-menu {
  height: 0;
  overflow: hidden;
}
</style>
