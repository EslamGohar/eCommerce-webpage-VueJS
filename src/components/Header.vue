<template>
  <nav>
    <div class="wrapper-icons" id="wrapper">
      <ul class="burger-icon">
        <li>
          <a href="#wrapper">
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

      <div class="left-icons">
        <a href="#">
          <span class="material-icons-outlined">calendar_today</span>
        </a>
        <a href="#">
          <span class="material-icons-outlined">chat_bubble_outline</span>
        </a>
        <a href="#"><span class="material-icons-outlined">mail</span></a>
        <a href="#"><span class="material-icons-outlined">add_task</span></a>
        <a href="#"><span class="material-icons-outlined">star_border</span></a>
      </div>

      <div class="right-icons">
        <ul>
          <div class="options">
            <li>
              <a href="#">
                <img src="../assets/united-states.svg" alt="language" />
                <span class="text">English</span>
              </a>
            </li>
            <li>
              <a href="#">
                <span
                  @click.prevent="changeTheme"
                  class="material-icons-outlined"
                  id="icon"
                >
                  dark_mode
                </span>
              </a>
            </li>
            <li>
              <a href="#">
                <span class="material-icons-outlined">search</span>
              </a>
            </li>
            <li>
              <a href="#">
                <span class="material-icons-outlined">shopping_cart</span>
                <span class="cart-badge">5</span>
              </a>
            </li>
            <li style="margin-left: -20px">
              <a href="#">
                <span class="material-icons-outlined">notifications</span>
                <span class="notification-badge">6</span>
              </a>
            </li>
          </div>
          <li class="profile-info">
            <a href="#">
              <div class="temp">
                <img
                  src="https://www.pngitem.com/pimgs/m/206-2067982_thinking-boy-clipart-and-cliparts-for-free-transparent.png"
                  alt="avatar"
                  class="img-circle-small"
                />
                <p class="user-name">John Doe</p>
                <span class="user-role">admin</span>
                <span class="status topRight"></span>
              </div>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "navgation-component",
  data() {
    return {
      theme: "",
    };
  },
  methods: {
    changeTheme() {
      let icon = document.getElementById("icon");
      document.body.classList.toggle("dark-theme");
      if (document.body.classList.contains("dark-theme")) {
        icon.innerHTML = `
            <span class="material-icons-outlined">
              light_mode
            </span>
            `;
      } else {
        icon.innerHTML = `
          <span class="material-icons-outlined">
            dark_mode
          </span>
          `;
      }
    },
  },
};
</script>

<style scoped>
nav {
  position: fixed;
  right: 0;
  width: calc(100% - 4rem - 260px);
  height: 63px;
  margin: 1.3rem 2rem 0;
  border-radius: 0.428rem;
  background-color: var(--bg-white);
  box-shadow: 0 4px 24px 0 rgb(34 41 47 / 10%);
  z-index: 1000;
}

@media screen and (max-width: 650px) {
  nav .wrapper-icons {
    text-align: center;
    margin-left: 15px;
    margin-right: 1.2rem;
  }
}

.wrapper-icons {
  display: flex;
  padding: 0.8rem 1rem;
  align-items: center;
}

@media screen and (max-width: 700px) {
  .wrapper-icons .left-icons {
    display: none;
  }
}

.burger-icon {
  display: none;
  list-style: none;
  color: var(--primary-text-color);
}

@media screen and (max-width: 700px) {
  .burger-icon {
    display: block;
    position: absolute;
    top: 20px;
    left: 25px;
    color: var(--primary-text-color);
  }
}

.left-icons {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 22px;
}

.left-icons a {
  text-decoration: none;
  color: var(--primary-text-color);
}

.left-icons a:last-child {
  color: #ff9f43;
}

.left-icons span {
  padding-left: 12px;
  font-size: 1.35rem;
}

.right-icons {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  margin-left: auto;
}

.options {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 37px;
  right: 177px;
}

.options img {
  width: 22px;
  height: 19px;
  position: absolute;
  top: 5px;
  border: 0;
}

.right-icons ul {
  list-style: none;
}

.right-icons a {
  text-decoration: none;
  display: flex;
  margin-left: 15px;
  color: var(--primary-text-color);
}

.right-icons span.text {
  padding-top: 3px;
  padding-left: 27px;
  font-size: 14px;
}

.right-icons .cart-badge {
  width: 19px;
  height: 19px;
  position: relative;
  right: 15px;
  bottom: 9px;
  text-align: center;
  color: var(--bg-white);
  background-color: var(--badge);
  border: 1px solid var(--badge);
  border-radius: 50%;
  font-size: 11px;
  font-weight: bold;
}

.right-icons .notification-badge {
  width: 19px;
  height: 19px;
  position: relative;
  right: 15px;
  bottom: 9px;
  text-align: center;
  color: var(--bg-white);
  background-color: #ea5455;
  border: 1px solid #ea5455;
  border-radius: 50%;
  font-size: 11px;
  font-weight: bold;
}

.right-icons .profile-info {
  color: var(--primary-text-color);
  text-align: right;
  display: flex;
}

.right-icons .user-name {
  display: flex;
  flex-direction: column;
  text-align: right;
  position: relative;
  right: 50px;
  bottom: 50px;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

@media screen and (max-width: 575px) {
  .user-name {
    display: none;
  }
}

.user-role {
  font-size: 12px;
  position: relative;
  right: 50px;
  bottom: 50px;
}

.img-circle-small {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  overflow: hidden;
}

.status {
  height: 10px;
  width: 10px;
  position: absolute;
  bottom: 0;
  right: 0;
  border-radius: 50%;
  border: 1px solid var(--bg-white);
  margin-bottom: 2px;
  background-color: rgb(24, 216, 24);
}

.temp {
  position: relative;
  top: 0;
  right: 10px;
}

.topRight {
  top: 30px;
  right: 0;
}

@media screen and (max-width: 1200px) {
  nav {
    width: calc(100% - 4rem);
  }
}

@media screen and (max-width: 650px) {
  nav {
    width: calc(100% - 2rem);
  }
}
</style>
