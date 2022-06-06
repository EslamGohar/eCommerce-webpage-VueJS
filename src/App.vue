<template>
  <div id="app" v-cloak>
    <sidebar-nav />
    <Header />
    <breadcrumb />
    <search-product />
    <footer-component />

    <!-- Buy Now Button -->
    <div class="buy-now">
      <a href="#">Buy Now</a>
    </div>

    <!-- Scroll to top -->
    <div class="btn-scroll-to-top" v-show="scroY > 250">
      <button type="button" class="btn" @click="goToTop">
        <span class="material-icons-outlined"> arrow_upward </span>
      </button>
    </div>
  </div>
</template>

<script>
// import Navbar from "./components/Navbar.vue";
import SidebarNav from "./components/SidebarNav.vue";
import Header from "./components/Header.vue";
import Breadcrumb from "./components/Breadcrumb.vue";
import SearchProduct from "./components/SearchProduct.vue";
import FooterComponent from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    SidebarNav,
    Header,
    Breadcrumb,
    SearchProduct,
    FooterComponent,
  },

  data() {
    return {
      scroTimer: 0,
      scroY: 0,
    };
  },

  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },

  methods: {
    handleScroll() {
      if (this.scroTimer) return;
      this.scroTimer = setTimeout(() => {
        this.scroY = window.scrollY;
        clearTimeout(this.scroTimer);
        this.scroTimer = 0;
      }, 300);
    },
    goToTop() {
      window.scrollTo({
        top: 0,
        behavior: "smooth",
      });
    },
  },
};
</script>

<style>
:root {
  --bg-light: #f6f6f6;
  --bg-dark: #161d31;
  --bg-white: #fff;
  --primary-text-color: #6e6b7b;
  --secondary-text-color: #4f759b;
  --badge: #7367f0;
  --btn-light: #ebe8e8;
  --btn-color: #2a2e30;
}

.dark-theme {
  --bg-light: #161d31;
  --bg-white: #283046;
  --primary-text-color: #b4b7bd;
  --btn-light: #161d31;
  --btn-color: #fff;
}

* {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  min-height: 100vh;
  font-family: "Montserrat", sans-serif;
  background-color: var(--bg-light);
  color: var(--secondary-text-color);
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
}

.buy-now {
  position: fixed;
  bottom: 45px;
  right: 80px;
  z-index: 1031;
}

.buy-now a {
  border-color: #ea5455;
  background-color: #ea5455;
  text-align: center;
  border: 1px solid transparent;
  padding: 0.6rem 1.3rem;
  border-radius: 0.358rem;
  color: #fff;
  font-weight: 500;
  font-size: 14px;
  text-decoration: none;
  box-shadow: 0 1px 20px 1px #ea5455;
  transition: all 0.3s;
}

.buy-now:hover a {
  box-shadow: none;
}

.btn-scroll-to-top {
  position: fixed;
  bottom: 35px;
  right: 30px;
  opacity: 1;
  z-index: 99;
  -webkit-transition: all 0.5s ease;
  transition: all 0.5s ease;
}

.btn-scroll-to-top .btn {
  background-color: var(--badge);
  border: 1px solid var(--badge);
  padding: 0.57rem 0.7rem;
  border-radius: 0.3rem;
  cursor: pointer;
}

.btn-scroll-to-top .btn:hover {
  box-shadow: 0 3px 15px 3px rgb(79 69 190 / 70%);
}

.btn-scroll-to-top .btn span {
  color: #fff;
  font-size: 16px;
  font-weight: 400;
}

[v-cloak] {
  display: none;
}
</style>
