<template>
  <nav class="navbar" :class="{ show: showSidebar }">
    <div class="navbar-logo">
      <a href="#">
        <img src="../assets/logo.svg" alt="brand-logo" />
        <h2 class="navbar-title" v-show="showTitle">Vuexy</h2>
      </a>
    </div>

    <div class="control" @click="showNav">
      <span class="material-icons-outlined"> keyboard_double_arrow_right </span>
    </div>

    <!-- <div class="navigation-icons">
      <span class="material-icons-outlined"> home </span>
      <span class="material-icons-outlined"> more_horiz </span>
      <span class="material-icons-outlined"> email </span>
      <span class="material-icons-outlined"> chat_bubble_outline </span>
      <span class="material-icons-outlined"> checklist </span>
      <span class="material-icons-outlined"> calendar_today </span>
      <span class="material-icons-outlined"> description </span>
      <span class="material-icons-outlined"> shopping_cart </span>
      <span class="material-icons-outlined"> person_outline </span>
    </div>

    <div class="navigation-links">
      <div v-show="showLink">Dashboards</div>
      <div v-show="showLink">Email</div>
      <div v-show="showLink">Chat</div>
      <div v-show="showLink">Todo</div>
      <div v-show="showLink">Calender</div>
      <div v-show="showLink">Invoice</div>
      <div v-show="showLink">eCommerce</div>
      <div v-show="showLink">User</div>
    </div> -->

    <ul class="navbar-menu">
      <li>
        <a href="#">
          <span class="material-icons-outlined"> home </span>
          <span v-show="showLink">Dashboards</span>
          <div class="badge" v-show="showLink">2</div>
          <span
            class="material-icons-outlined"
            @click="show = !show"
            v-show="showLink"
          >
            chevron_right
          </span>
        </a>

        <ul class="dropdown-list" v-show="showLink">
          <li class="list-item">
            <a href="#">
              <span class="list-title">eCommerce</span>
            </a>
          </li>
          <li class="list-item">
            <a href="#">
              <span class="list-title">Analytics</span>
            </a>
          </li>
        </ul>
      </li>
    </ul>

    <div class="apps-pages">
      <span class="apps-title" v-show="showLink">apps & pages</span>
      <ul class="apps-items">
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined"> email </span>
            <span v-show="showLink">Email</span>
          </a>
        </li>
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined">chat_bubble_outline</span>
            <span v-show="showLink">Chat</span>
          </a>
        </li>
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined"> checklist </span>
            <span v-show="showLink">Todo</span>
          </a>
        </li>
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined"> calendar_today </span>
            <span v-show="showLink">Calender</span>
          </a>
        </li>
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined"> description </span>
            <span v-show="showLink">Invoice</span>
          </a>
        </li>
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined"> shopping_cart </span>
            <span v-show="showLink">eCommerce</span>
          </a>
        </li>
        <li>
          <a href="#" class="item-icons">
            <span class="material-icons-outlined"> person_outline </span>
            <span v-show="showLink">User</span>
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: "navbar-component",
  data() {
    return {
      showSidebar: true,
      showLink: true,
      showTitle: false,
      showDropdown: false,
    };
  },
  methods: {
    showNav() {
      if (this.showSidebar) {
        this.showSidebar = false;
        setTimeout(() => {
          this.showLink = false;
          this.showTitle = false;
        }, 200);
      } else {
        this.showSidebar = true;
        setTimeout(() => {
          this.showLink = true;
          this.showTitle = true;
        }, 300);
      }
    },
  },
};
</script>

<style scoped>
.navbar {
  width: 80px;
  height: 100%;
  position: fixed;
  padding: 10px 0;
  background-color: var(--bg-white);
  box-shadow: 0 0 15px 0 rgb(34 41 47 / 5%);
  transition: all 0.5s ease-in-out;
  z-index: 999;
}

.control {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  margin-bottom: 30px;
}

.control span {
  font-size: 1.8rem;
  cursor: pointer;
  color: var(--badge);
  transition: all 0.4s ease-in-out;
  position: absolute;
  right: 25px;
  top: 36px;
}

.navigation-icons {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 50px;
}

.navigation-icons > span {
  font-size: 1.45rem;
  padding: 12px 0;
  cursor: pointer;
  color: var(--primary-text-color);
  transition: all 0.5s ease-in-out;
}

.show {
  width: 265px;
  background-color: var(--bg-white);
}

.show .control span {
  color: var(--badge);
  transform: rotateZ(-180deg);
}

.navbar-logo {
  display: flex;
  align-items: center;
  padding-top: 25px;
}

.navbar-logo a {
  display: flex;
  text-decoration: none;
  padding-left: 20px;
}

.navbar-logo img {
  max-width: 38px;
}

.navbar-title {
  padding-left: 14px;
  font-weight: 600;
  font-size: 1.3rem;
  letter-spacing: 0.02rem;
  color: var(--badge);
}

.navbar-toggle-icon {
  position: relative;
  bottom: 20px;
  left: 100px;
  text-decoration: none;
  transition: all 0.5s ease-in-out;
}

.navbar-toggle-icon span {
  font-size: 1.35rem;
  color: var(--badge);
  /* transition: all 0.5s ease-in-out; */
}

.navbar-menu {
  display: flex;
  justify-content: center;
  align-items: center;
  list-style: none;
}

.navbar-menu li {
  margin-right: 40px;
}

.navbar-menu a {
  text-decoration: none;
  color: var(--primary-text-color);
}

.navbar-menu span {
  position: relative;
  width: 40px;
}

.navbar-menu span:first-child {
  position: absolute;
  top: 86px;
  left: 27px;
}

.badge {
  width: 20px;
  height: 19px;
  position: absolute;
  left: 200px;
  top: 87px;
  color: #ff9f43;
  background-color: rgba(205, 118, 35, 0.1);
  border: 1px solid rgba(205, 118, 35, 0.02);
  border-radius: 50%;
  font-size: 13px;
  font-weight: bold;
}

.navbar-menu span:last-child {
  position: absolute;
  left: 228px;
  top: 87px;
  font-size: 19px;
}

.dropdown-list {
  list-style-type: circle;
  position: absolute;
  top: 85px;
  left: 60px;
  color: #777;
}

.dropdown-list .list-item {
  position: absolute;
  left: 0;
  top: 50px;
}

.list-item a .list-title {
  left: 0;
  top: 0;
  font-size: 15px;
  letter-spacing: 0.4px;
  margin-left: 12px;
}

.list-item:last-child {
  margin-top: 40px;
}

.apps-pages span {
  position: relative;
  right: 20px;
  bottom: 0;
}

.apps-pages span.apps-title {
  font-weight: 500;
  font-size: 13px;
  color: var(--primary-text-color);
  position: relative;
  right: 50px;
  top: 130px;
  text-transform: uppercase;
}

.apps-pages .apps-items {
  list-style: none;
  position: absolute;
  top: 280px;
  left: 50px;
}

.apps-pages .item-icons {
  text-decoration: none;
  color: var(--primary-text-color);
}

.apps-pages .item-icons span:first-child {
  font-size: 22px;
  margin: 15px 0;
}

.apps-pages .item-icons span:last-child {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  left: 50px;
  bottom: 36px;
}
</style>
