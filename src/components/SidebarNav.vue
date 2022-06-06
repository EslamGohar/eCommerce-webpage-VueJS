<template>
  <ul v-show="!isMobile" class="burger-icon" @click="isMobile = !isMobile">
    <li>
      <a>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="21px"
          height="21px"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="feather feather-menu"
        >
          <line x1="3" y1="12" x2="21" y2="12"></line>
          <line x1="3" y1="6" x2="21" y2="6"></line>
          <line x1="3" y1="18" x2="21" y2="18"></line>
        </svg>
      </a>
    </li>
  </ul>

  <div v-show="isMobile" @click="isMobile = !isMobile" class="overlay"></div>

  <aside class="sidenav-container" :class="isMobile && 'mobile'">
    <div class="sidenav-header">
      <a href="#">
        <span>
          <img src="../assets/logo.svg" alt="brand-logo" />
        </span>
        <h2>Vuexy</h2>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20px"
          height="20px"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="d-none d-xl-block collapse-toggle-icon feather feather-disc"
        >
          <circle cx="12" cy="12" r="10"></circle>
          <circle cx="12" cy="12" r="3"></circle>
        </svg>
      </a>
    </div>

    <div class="sidenav-menu">
      <ul>
        <SidebarNavItem
          itemText="Dashboards"
          :itemsInside="dashboardsItems"
          isOpen="open"
        >
          <span class="material-icons-outlined"> home </span>
          <div class="badge">2</div>
          <span class="cheveron material-icons-outlined"> expand_more </span>
        </SidebarNavItem>

        <div class="apps-pages">
          <span class="apps-title">apps & pages</span>

          <SidebarNavItem itemText="Email">
            <span class="material-icons-outlined"> email </span>
          </SidebarNavItem>

          <SidebarNavItem itemText="Chat">
            <span class="material-icons-outlined">chat_bubble_outline</span>
          </SidebarNavItem>

          <SidebarNavItem itemText="Todo">
            <span class="material-icons-outlined"> checklist </span>
          </SidebarNavItem>

          <SidebarNavItem itemText="Calendar">
            <span class="material-icons-outlined"> calendar_today </span>
          </SidebarNavItem>

          <SidebarNavItem itemText="Invoice">
            <span class="material-icons-outlined"> description </span>
          </SidebarNavItem>

          <SidebarNavItem
            itemText="eCommerce"
            :itemsInside="eCommerceItems"
            isOpen="open"
          >
            <span class="cart material-icons-outlined"> shopping_cart </span>
            <span class="rightArrow material-icons-outlined">
              expand_more
            </span>
          </SidebarNavItem>

          <SidebarNavItem itemText="User">
            <span class="material-icons-outlined"> person_outline </span>
          </SidebarNavItem>

          <SidebarNavItem itemText="Pages">
            <span class="material-icons-outlined"> description </span>
          </SidebarNavItem>
        </div>
      </ul>
    </div>
  </aside>
</template>

<script>
import SidebarNavItem from "./SidebarNavItem.vue";

export default {
  name: "SidebarNav",

  components: {
    SidebarNavItem,
  },

  data() {
    return {
      dashboardsItems: ["eCommerce", "Analytics"],
      eCommerceItems: ["Shop", "Details", "Wishlist", "Checkout"],
      isMobile: false,
    };
  },
};
</script>

<style scoped>
.sidenav-container {
  z-index: 2000;
  position: fixed;
  height: 100%;
  overflow: hidden;
  background-color: var(--bg-white);
  width: 275px;
  transition: 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  box-shadow: 0 0 15px 0 rgb(34 41 47 / 5%);
  overflow-y: scroll;
}

.sidenav-header {
  margin-top: 1.35rem;
  padding: 0.35rem 1rem 0.3rem 1.64rem;
}

.sidenav-header a {
  display: flex;
  text-decoration: none;
}

.sidenav-header img {
  max-width: 36px;
}

.sidenav-header h2 {
  color: #7367f0;
  font-weight: 600;
  letter-spacing: 0.01rem;
  font-size: 1.25rem;
  padding-left: 1rem;
}

.sidenav-header svg {
  margin-left: 73px;
  color: #7367f0;
  margin-top: 4px;
}

@media screen and (max-width: 1200px) {
  .sidenav-container {
    display: none;
  }
}

.burger-icon {
  cursor: pointer;
  position: absolute;
  top: 37px;
  left: 48px;
  z-index: 1000;
  list-style-type: none;
}

@media screen and (max-width: 650px) {
  .burger-icon {
    top: 38px;
    left: 35px;
  }
}

@media screen and (min-width: 1200px) {
  .burger-icon {
    display: none;
  }
}

@media screen and (max-width: 1200px) {
  .mobile {
    display: block;
  }
}

.overlay {
  z-index: 1000;
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  background-color: rgba(34, 34, 34, 0.3);
}

.badge {
  width: 20px;
  height: 19px;
  position: absolute;
  left: 200px;
  top: 75px;
  color: #ff9f43;
  background-color: rgba(205, 118, 35, 0.1);
  border: 1px solid rgba(205, 118, 35, 0.02);
  border-radius: 50%;
  font-size: 13px;
  font-weight: bold;
  text-align: center;
}

.sidenav-menu .cheveron {
  position: absolute;
  left: 220px;
  top: 75px;
  font-size: 20px;
}

.apps-pages {
  margin: 2.286rem 0;
}

.apps-pages span {
  font-size: 20px;
}

.apps-pages .apps-title {
  font-weight: 500;
  font-size: 14px;
  color: var(--primary-text-color);
  position: relative;
  right: -25px;
  bottom: 10px;
  text-transform: uppercase;
}

.apps-pages .apps-items {
  position: absolute;
  top: 280px;
  left: 50px;
}

.apps-pages span.cart {
  position: inherit;
  margin-right: -20px;
}

.apps-pages .rightArrow {
  position: relative;
  left: 190px;
  top: 3px;
  font-size: 20px;
}
</style>
