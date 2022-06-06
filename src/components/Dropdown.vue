<template>
  <div class="dropdown">
    <button @click="toggleShow" class="dropbtn" ref="dropdown">
      {{ title }}
      <span class="material-icons-outlined"> {{ icon }} </span>
    </button>

    <div v-if="showMenu" class="menu">
      <div
        class="menu-item"
        v-for="(item, index) of this.items"
        :key="index"
        @click="sortPrice(item)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dropdown-menu",

  props: {
    title: String,
    icon: String,
    items: {
      type: Array,
      required: true,
    },
  },

  data() {
    return {
      showMenu: false,
    };
  },

  created() {
    document.addEventListener("click", this.setClickOutside);
  },

  unmounted() {
    document.removeEventListener("click", this.setClickOutside);
  },

  methods: {
    toggleShow: function () {
      this.showMenu = !this.showMenu;
    },

    setClickOutside: function (e) {
      let el = this.$refs.dropdown;
      let target = e.target;
      if (el !== target && !el.contains(target)) {
        this.showMenu = false;
      }
    },

    sortPrice: function (item) {
      this.$emit("sort", item);
      this.toggleShow();
    },
  },
};
</script>

<style scoped>
.dropdown {
  position: absolute;
  top: 170px;
  right: 148px;
  display: inline-block;
}

.dropbtn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 120px;
  height: 38px;
  font-size: 15px;
  letter-spacing: 0.5px;
  border: 1px solid var(--badge);
  border-radius: 5px;
  color: var(--badge);
  background-color: transparent;
  cursor: pointer;
}

.dropbtn span {
  position: relative;
  left: 10px;
  font-size: 19px;
}

.dropbtn:hover,
.dropbtn:focus {
  background-color: rgba(115, 103, 240, 0.2);
}

.menu {
  display: block;
  margin-top: 5px;
  min-width: 138px;
  position: absolute;
  right: 0;

  background-color: var(--bg-white);
  background-clip: padding-box;
  border: 1px solid rgba(34, 41, 47, 0.05);
  border-radius: 5px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  text-align: left;
  cursor: pointer;
  z-index: 1;
}

.menu-item {
  color: var(--primary-text-color);
  font-size: 14px;
  padding: 8px 16px;
  margin: 6px 0;
  text-decoration: none;
  display: block;
}

.menu-item:hover {
  background-color: var(--bg-light);
  color: var(--badge);
  padding: 8px 16px;
  margin: 6px 0;
  border-radius: 0px;
  cursor: pointer;
}
</style>
