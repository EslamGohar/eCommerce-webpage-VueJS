<template>
  <header>
    <div class="breadcrumb-container">
      <h2 class="title">Shop</h2>

      <div class="breadcrumb">
        <ul class="breadcrumb-items">
          <li>
            <a href="#">
              <span class="material-icons-outlined"> home </span>
            </a>
          </li>
          <li><span class="material-icons-outlined"> navigate_next </span></li>
          <li><a href="#">ECommerce</a></li>
          <li><span class="material-icons-outlined"> navigate_next </span></li>
          <li>Shop</li>
        </ul>
      </div>
    </div>

    <div class="settings">
      <div class="dropdown">
        <button class="dropbtn" @click="toggleShow">
          <span class="material-icons-outlined"> settings </span>
        </button>
        <div class="dropdown-content" v-if="showMenu">
          <a href="#">
            <span class="material-icons-outlined"> task </span>
            <span>Todo</span>
          </a>
          <a href="#">
            <span class="material-icons-outlined"> chat_bubble_outline </span>
            <span>Chat</span>
          </a>
          <a href="#">
            <span class="material-icons-outlined"> email </span>
            <span>Email</span>
          </a>

          <a href="#">
            <span class="material-icons-outlined">calendar_today</span>
            <span>Calender</span>
          </a>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "breadcrumb-component",

  data() {
    return {
      showMenu: false,
    };
  },

  methods: {
    toggleShow: function () {
      this.showMenu = !this.showMenu;
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.breadcrumb-container {
  display: flex;
  align-items: center;
  margin-bottom: 1.5rem;
  position: absolute;
  top: 110px;
  left: 290px;
}

.title {
  font-weight: 500;
  color: var(--primary-text-color);
  border-right: 1px solid #d6dce1;
  padding-right: 1rem;
}

@media screen and (max-width: 650px) {
  .breadcrumb {
    position: absolute;
    top: 110px;
    left: 290px;
    display: none;
    text-align: center;
  }

  .breadcrumb-container {
    display: flex;
    align-items: flex-start;
    margin-bottom: 1.5rem;
    position: absolute;
    top: 110px;
    left: 0px;
  }
}

.breadcrumb-items {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  padding: 0.3rem 0.7rem;
  list-style: none;
}

.breadcrumb-items li {
  padding-right: 1px;
  font-size: 14px;
}

.breadcrumb-items li:last-child {
  color: var(--primary-text-color);
}

.breadcrumb-items a {
  text-decoration: none;
  color: var(--badge);
  font-size: 14px;
}

.breadcrumb-items span {
  font-size: 20px;
  color: #636363;
}

.breadcrumb-items a span:first-child {
  color: var(--badge);
}

.settings {
  display: flex;
  justify-content: flex-end;
}

.dropdown {
  position: absolute;
  top: 112px;
  right: 35px;
}

.dropbtn {
  background-color: var(--badge);
  color: var(--bg-white);
  padding: 11px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.dropbtn span {
  font-size: 18px;
  color: var(--btn-white);
}

.dropdown-content {
  position: absolute;
  right: 5%;
  margin-top: 8px;
  background-color: var(--bg-white);
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.05);
  border-radius: 5px;
  z-index: 1;
}

.dropdown-content a {
  font-size: 14px;
  color: var(--primary-text-color);
  padding: 11px 5px;
  text-decoration: none;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

.dropdown-content a span {
  font-size: 16px;
  padding-left: 12px;
}

.dropdown-content a:hover {
  background-color: var(--bg-light);
  color: var(--badge);
}

.show {
  display: block;
}

.dropdown:hover .dropbtn {
  box-shadow: 0 8px 25px -8px var(--badge);
}
</style>
