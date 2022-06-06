<template>
  <section class="ecommerce-content">
    <div>
      <filters @filter-price="filterByPrice" />
    </div>

    <!-- Dropdow menu -->
    <dropdown
      :title="sortedBy"
      :items="arrangements"
      :icon="material_icons"
      @sort="sortedProducts"
    ></dropdown>

    <!-- Layout Buttons -->
    <div class="btnGroup">
      <button
        class="btn1"
        @click="layout = 'grid'"
        :class="{ active: layout == 'grid' }"
      >
        <span class="material-icons"> grid_view </span>
      </button>

      <button
        class="btn2"
        @click="layout = 'list'"
        :class="{ active: layout == 'list' }"
      >
        <span class="material-icons"> list </span>
      </button>
    </div>

    <!-- Search bar -->
    <div class="ecommerce-header">
      <div class="search-counts">{{ numOfFilteredProducts }} results found</div>
    </div>
    <div class="searchbar">
      <input
        type="text"
        v-model="searchValue"
        placeholder="Search Product"
        @input="filterProducts"
      />
      <span class="material-icons-outlined"> search </span>
    </div>

    <!-- Grid View Layout for Products Content -->
    <div class="grid-view" v-if="layout === 'grid'">
      <div
        v-for="prod of filteredData.slice(0, 12)"
        :key="prod.id"
        class="card"
      >
        <div class="card-body">
          <div class="item-img">
            <a href="#">
              <img :src="prod.img" :alt="prod.name" class="product-image" />
            </a>
          </div>

          <div class="item-rating">
            <ul>
              <li><span class="material-icons"> star </span></li>
              <li><span class="material-icons"> star </span></li>
              <li><span class="material-icons"> star </span></li>
              <li>
                <span class="material-icons-outlined"> star_border </span>
              </li>
            </ul>
          </div>

          <h5 class="item-price">${{ prod.price }}</h5>
          <div class="item-details">
            <h4 class="item-title">{{ prod.name }}</h4>
            <p class="item-description">{{ prod.discription }}</p>
          </div>
        </div>

        <div class="item-options">
          <a href="#" class="wishlist">
            <span class="material-icons-outlined"> favorite_border </span>
            <span>Wishist</span>
          </a>
          <a href="#" class="addCart">
            <span class="material-icons-outlined"> shopping_cart </span>
            <span>View In Cart</span>
          </a>
        </div>
      </div>
    </div>

    <!-- List View Layout for Products Content -->
    <div class="list-view" v-if="layout === 'list'">
      <div class="box" v-for="prod of filteredData.slice(0, 12)" :key="prod.id">
        <div class="prod-image">
          <a href="#">
            <img :src="prod.img" :alt="prod.name" />
          </a>
        </div>

        <div class="box-body">
          <h4 class="prod-name">{{ prod.name }}</h4>
          <p class="company">
            By: <a href="#" class="prod-brand"> {{ prod.brand }}</a>
          </p>
          <div class="prod-rating">
            <ul>
              <li><span class="material-icons"> star </span></li>
              <li><span class="material-icons"> star </span></li>
              <li><span class="material-icons"> star </span></li>
              <li>
                <span class="material-icons-outlined"> star_border </span>
              </li>
            </ul>
          </div>
          <p class="prod-description">{{ prod.discription }}</p>
        </div>

        <div class="box-options">
          <div class="prod-cost">
            <h5 class="price">${{ prod.price }}</h5>
          </div>

          <a href="#" class="wishlist-btn">
            <span class="material-icons-outlined"> favorite_border </span>
            <span>Wishist</span>
          </a>
          <a href="#" class="addCart-btn">
            <span class="material-icons-outlined"> shopping_cart </span>
            <span>View In Cart</span>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Dropdown from "./Dropdown.vue";
import Filters from "./Filters.vue";

export default {
  name: "search-bar",
  components: {
    Filters,
    Dropdown,
  },

  data() {
    return {
      productData: require("@/data/store-data.json"),
      layout: "grid",
      sortedBy: "Featured",
      arrangements: ["Featured", "Lowest", "Highest"],
      material_icons: "expand_more",
      filteredData: [],
      searchValue: "",
      selectedPrice: null,
    };
  },

  computed: {
    // return number of search results
    numOfFilteredProducts: function () {
      return this.filteredData.length;
    },
  },

  methods: {
    filterProducts() {
      if (this.searchValue != "" && this.searchValue) {
        this.filteredData = this.productData.products.filter((prod) => {
          return prod.name
            .toLowerCase()
            .includes(this.searchValue.toLowerCase());
        });
      }
    },

    // return the sort of products prices
    sortedProducts(item) {
      this.sortedBy = item;

      let tempProducts = this.productData.products;
      if (item === "Featured") {
        this.filteredData = tempProducts.sort((a, b) => (a.id < b.id ? 1 : -1));
      } else if (item === "Highest") {
        this.filteredData = tempProducts.sort((a, b) => b.price - a.price);
      } else if (item === "Lowest") {
        this.filteredData = tempProducts.sort((a, b) => a.price - b.price);
      }
      return this.filteredData;
    },

    // return multi price ranges for the products
    filterByPrice(price) {
      this.selectedPrice = price;
      let tempProducts = this.productData.products;

      if (this.selectedPrice) {
        this.filteredData = tempProducts.filter(
          (item) => item.price >= price.min && item.price <= price.max
        );
      } else this.filteredData = tempProducts;
    },
  },

  mounted() {
    this.filteredData = [...this.productData.products];
  },
};
</script>

<style scoped>
.ecommerce-content {
  display: flex;
  justify-content: center;
  align-items: center;
}

.ecommerce-header {
  position: absolute;
  top: 177px;
  left: 575px;
}

.search-counts {
  font-size: 14px;
  font-weight: 500;
  color: var(--primary-text-color);
  letter-spacing: 0.4px;
}

.searchbar {
  display: flex;
  justify-content: center;
  background-color: var(--bg-white);
  position: absolute;
  top: 219px;
  right: 23px;
  border: 3px solid var(--bg-white);
  border-radius: 4px;
  box-shadow: 0 2px 8px 0 rgb(34 41 47 / 14%);
  margin-left: 10px;
}

@media screen and (max-width: 768px) {
  .searchbar {
    width: 100%;
  }
}

.searchbar input {
  width: 725px;
  height: 42px;
  border: 3px solid var(--bg-white);
  background: var(--bg-white);
  outline: none;
}

.searchbar input[placeholder] {
  color: var(--primary-text-color);
  font-size: 14px;
  font-weight: 500;
  padding-left: 12px;
}

.searchbar span {
  position: relative;
  top: 12px;
  right: 12px;
  color: #b9b9c3;
  font-size: 21px;
}

.btnGroup {
  position: absolute;
  top: 170px;
  right: 35px;
}

.btnGroup button {
  display: inline-block;
  width: 50px;
  height: 38px;
  font-size: 15px;
  letter-spacing: 0.5px;
  border: 1px solid #7367f0;
  border-radius: 5px;
  color: var(--badge);
  background-color: transparent;
  cursor: pointer;
}

.btnGroup .btn1 {
  border-right: 3px;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

.btnGroup .btn2 {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}

.btn1.active {
  background-color: rgba(115, 103, 240, 0.2);
}

.btn2.active {
  background-color: rgba(115, 103, 240, 0.2);
}

.btn1:hover,
.btn1:focus,
.btn2:hover,
.btn2:focus {
  background-color: rgba(115, 103, 240, 0.2);
}

/*** Layout Style ***/
.grid-view {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 20px;
  grid-row-gap: 10px;
  position: relative;
  left: 276px;
  bottom: 12px;
  margin: 295px;
}

@media screen and (max-width: 990px) {
  .grid-view {
    grid-template-columns: 1fr 1fr;
  }
}

@media screen and (max-width: 575px) {
  .grid-view {
    grid-template-columns: 1fr;
  }
}

.card {
  width: 230px;
  margin: 12px 6px;
  border-radius: 8px;
  box-shadow: 0 4px 24px 0 rgb(34 41 47 / 10%);
  background-color: var(--bg-white);
  transition: 0.3s all ease-in-out;
}

.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 2px 8px 2px rgb(34 41 47 / 30%);
}

.card-body .product-image {
  width: 220px;
  padding: 25px 0;
}

.card-body .item-rating ul {
  display: flex;
  justify-content: flex-start;
  list-style-type: none;
}

.card-body .item-rating span {
  font-size: 19px;
  color: #ff9f43;
  margin-left: 5px;
}

.card-body .item-details .item-title {
  width: 166px;
  padding-top: 10px;
  padding-bottom: 10px;
  margin-top: -15px;
  margin-left: 10px;
  font-weight: 600;
  font-size: 14px;
  color: var(--primary-text-color);
  text-transform: capitalize;
  text-align: left;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}

.item-details .item-title:hover {
  color: var(--badge);
  cursor: pointer;
}

.item-details .item-description {
  text-align: left;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  font-size: 12px;
  color: var(--primary-text-color);
  margin-left: 11px;
}

.item-price {
  text-align: right;
  font-weight: 600;
  color: var(--primary-text-color);
  font-size: 14px;
  position: relative;
  bottom: 22px;
  margin-right: 12px;
}

.item-options a {
  text-decoration: none;
  color: var(--primary-text-color);
  font-weight: 500;
  display: block;
  padding: 10px;
}

.wishlist {
  text-align: center;
  font-size: 14px;
  padding: 11px 20px;
  margin-top: 20px;
  color: var(--btn-color);
  background-color: var(--bg-light);
}

.wishlist:hover {
  background-color: var(--btn-light);
}

.wishlist span {
  color: var(--btn-color);
  font-size: 15px;
  padding-left: 5px;
}

.addCart {
  text-align: center;
  font-size: 14px;
  padding: 5px 0;
  color: var(--bg-white);
  background-color: var(--badge);
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
}

.addCart span {
  color: var(--bg-white);
  font-size: 15px;
  padding-left: 5px;
}

/*** List view layout ***/
.list-view {
  display: flex;
  align-items: center;
  flex-flow: column wrap;
  position: relative;
  left: 276px;
  bottom: 0;
  margin: 295px;
}

.box {
  display: flex;
  height: 210px;
  margin-bottom: 30px;
  border-radius: 6px;
  background-color: var(--bg-white);
  box-shadow: 0 4px 24px 0 rgb(34 41 47 / 10%);
  transition: 0.3s all ease-in-out;
  overflow: hidden;
}

.box:hover {
  transform: translateY(-6px);
  box-shadow: 0 2px 8px 2px rgb(34 41 47 / 30%);
}

.box .prod-image {
  display: flex;
  align-items: center;
  justify-content: center;
}

.box .prod-image img {
  width: 190px;
}

.box-body {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  padding: 15px;
  border-right: 1px solid var(--btn-light);
}

.box-body .prod-name {
  width: 300px;
  margin-top: 12px;
  margin-bottom: 5px;
  font-size: 14px;
  font-weight: 600;
  color: var(--primary-text-color);
  text-align: left;
  text-transform: capitalize;

  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}

.box-body .prod-name:hover {
  color: var(--badge);
  cursor: pointer;
}

.box-body .company {
  margin: 0.3rem 0 0.5rem;
  font-size: 12.5px;
  color: var(--primary-text-color);
  text-transform: capitalize;
}

.box-body .prod-brand {
  font-weight: 600;
  color: var(--badge);
  text-decoration: none;
}

.box-body .prod-description {
  width: 330px;
  text-align: left;
  font-size: 12px;
  line-height: 17px;
  color: var(--primary-text-color);
  overflow: hidden;
  text-overflow: ellipsis;

  display: -webkit-box;
  -webkit-line-clamp: 5;
  -webkit-box-orient: vertical;
}

.box-options {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 200px;
  padding: 15px;

  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
}

.box-body .prod-rating ul {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 0.3rem;
  list-style-type: none;
}

.box-body .prod-rating span {
  font-size: 19px;
  color: #ff9f43;
}

.box-options .prod-cost {
  position: relative;
}

.prod-cost .price {
  margin-bottom: 0;
  color: var(--badge);
  font-size: 18px;
  font-weight: 500;
  letter-spacing: 1px;
}

.wishlist-btn {
  padding: 10px;
  margin: 14px;
  color: var(--btn-color);
  background-color: var(--bg-light);
  border-radius: 5px;
  text-decoration: none;
}

.wishlist-btn:hover {
  background-color: var(--btn-light);
}

.wishlist-btn span {
  color: var(--btn-color);
  font-size: 15px;
  padding-left: 5px;
}

.addCart-btn {
  padding: 10px;
  margin: 0 14px;
  color: var(--bg-white);
  background-color: var(--badge);
  border-radius: 5px;
  text-decoration: none;
}

.addCart-btn span {
  color: var(--bg-white);
  font-size: 15px;
  padding-left: 5px;
}

.addCart-btn:hover {
  box-shadow: 0 3px 15px 3px rgb(79 69 190 / 70%);
}
</style>
