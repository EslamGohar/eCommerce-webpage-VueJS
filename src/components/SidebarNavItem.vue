<template>
  <li class="item">
    <a href="#" @click="this.isClosed = !this.isClosed" :class="!isClosed">
      <div class="itemIcon">
        <slot />
      </div>
      <span class="itemTitle">{{ itemText }}</span>
    </a>
    <ul :class="isClosed && 'closed'" class="submenu">
      <li class="subitem" v-for="item in itemsInside" :key="item">
        <a :class="item === 'Shop' && 'highlighted'">
          <svg
            class="icon"
            xmlns="http://www.w3.org/2000/svg"
            width="16"
            height="16"
            viewBox="0 0 24 24"
            style="fill: currentColor; transform: ; msfilter: "
          >
            <path
              d="M5 12c0 3.859 3.14 7 7 7 3.859 0 7-3.141 7-7s-3.141-7-7-7c-3.86 0-7 3.141-7 7zm12 0c0 2.757-2.243 5-5 5s-5-2.243-5-5 2.243-5 5-5 5 2.243 5 5z"
            ></path>
          </svg>
          <span>{{ item }}</span>
        </a>
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  name: "SidebarNavItem",

  created() {
    this.toggleClosed();
  },

  data() {
    return {
      isClosed: true,
    };
  },

  props: {
    isOpen: {
      type: String,
    },
    itemsInside: {
      type: Array,
    },
    itemText: {
      type: String,
      required: true,
    },
  },

  methods: {
    toggleClosed() {
      if (this.isOpen === "open") {
        this.isClosed = !this.isClosed;
      }
    },
  },
};
</script>

<style scoped>
li .item {
  margin-top: 0.5rem;
  position: relative;
  white-space: nowrap;
  font-size: 1rem;
  cursor: pointer;
  list-style: none;
}

.arrow-down:after {
  transform: rotate(90deg);
}

.item a {
  display: flex;
  align-items: center;
  border-radius: 6px;
  margin: 0 15px;
  padding: 10px 15px 10px 15px;
  text-decoration: none;
  color: var(--primary-text-color);
}
/* 
.item a:hover {
  transform: translateX(6px);
} */

.itemIcon,
.itemTitle {
  margin-right: 10px;
}

.icon {
  margin-right: 1.1rem;
}

span {
  white-space: nowrap;
  font-size: 1.1rem;
  font-weight: 400;
}

.icon,
span {
  transition: all 0.5s ease;
}

.submenu {
  margin: 0 5px;
}

.subitem span {
  font-size: 1rem;
}

.highlighted {
  color: var(--bg-white);
  background-image: linear-gradient(
    118deg,
    rgb(115, 103, 240),
    rgba(115, 103, 240, 0.7)
  );
  box-shadow: 0 0 10px 1px rgba(115, 103, 240, 0.7);
}

.closed {
  display: none;
}
</style>
