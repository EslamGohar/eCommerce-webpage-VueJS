<template>
  <div class="sidebar">
    <h5 class="filter-heading">Filters</h5>
    <div class="sidebar-body">
      <h5 class="filter-title">Multi Range</h5>
      <div class="multi-range">
        <div class="multi-range-group" v-for="range in ranges" :key="range.lbl">
          <label :for="range.lbl">
            <input
              type="radio"
              :id="range.lbl"
              :value="{ min: range.min, max: range.max }"
              name="price"
              v-model="selectPrice"
              class="custom-control-input"
              @change="filterRangePrice"
            />
            {{ range.lbl }}
          </label>
        </div>
      </div>

      <h5 class="price-title">Price Range</h5>
      <div class="price-range">
        <div class="slidecontainer">
          <div class="range-slider">
            <input
              type="range"
              min="0"
              max="1000"
              step="1"
              v-model="sliderMin"
            />
            <input
              type="range"
              min="0"
              max="1000"
              step="1"
              v-model="sliderMax"
            />
          </div>
        </div>
      </div>

      <h5 class="categories-title">Categories</h5>
      <div class="product-categries">
        <div
          class="product-categries-group"
          v-for="category in Categories"
          :key="category.id"
        >
          <label :for="category.name">
            <input
              type="radio"
              class="custom-control-input"
              name="category"
              :id="category.name"
              :value="category.name"
              v-model="seletCategory"
            />
            {{ category.name }}
          </label>
        </div>
      </div>

      <h5 class="brands-title">Brands</h5>
      <div class="brands">
        <div class="brands-group" v-for="brand in Brands" :key="brand.id">
          <label :for="brand.lbl">
            <input
              type="radio"
              class="custom-control-input"
              name="brand"
              :id="brand.lbl"
              :value="brand.lbl"
              v-model="selectBrand"
            />
            {{ brand.lbl }}
          </label>
        </div>
      </div>

      <h5 class="rating-title">Ratings</h5>
      <div class="rating-list">
        <ul class="rating-list-items">
          <li>
            <a href="#">
              <span class="material-icons"> star </span>
              <span class="material-icons"> star </span>
              <span class="material-icons"> star </span>
              <span class="material-icons"> star </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="and-up">& Up</span>
            </a>
            <span class="rating-mount">160</span>
          </li>
          <li>
            <a href="#">
              <span class="material-icons"> star </span>
              <span class="material-icons"> star </span>
              <span class="material-icons"> star </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="and-up">& Up</span>
            </a>
            <span class="rating-mount">176</span>
          </li>
          <li>
            <a href="#">
              <span class="material-icons"> star </span>
              <span class="material-icons"> star </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="and-up">& Up</span>
            </a>
            <span class="rating-mount">291</span>
          </li>
          <li>
            <a href="#">
              <span class="material-icons"> star </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="material-icons-outlined"> star_border </span>
              <span class="and-up">& Up</span>
            </a>
            <span class="rating-mount">190</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Filters-component",

  data() {
    return {
      minAngle: 0,
      maxAngle: 1000,

      ranges: [
        { lbl: "All", min: 0, max: 1000000 },
        { lbl: "<= $10", min: 0, max: 10 },
        { lbl: "$10 - $100", min: 10, max: 100 },
        { lbl: "$100 - $500", min: 100, max: 500 },
        { lbl: ">= $500", min: 500, max: 1000000 },
      ],
      selectPrice: { min: 0, max: 1000000 },

      Categories: [
        { id: 1, name: "Appliances" },
        { id: 2, name: "Audio" },
        { id: 3, name: "Cameras & Camcorders" },
        { id: 4, name: "Car Electronics & GPS" },
        { id: 5, name: "Cell Phones" },
        { id: 6, name: "Computers & Tablets" },
        { id: 7, name: "Health, Fitness & Beauty" },
        { id: 8, name: "Office & School Supplies" },
        { id: 9, name: "TV & Home Theater" },
        { id: 10, name: "Video Games" },
      ],
      seletCategory: "",

      Brands: [
        { id: 1, lbl: "Insignia™" },
        { id: 2, lbl: "Samsung" },
        { id: 3, lbl: "Metra" },
        { id: 4, lbl: "HP" },
        { id: 5, lbl: "Apple" },
        { id: 6, lbl: "GE" },
        { id: 7, lbl: "Sony" },
        { id: 8, lbl: "Incipio" },
        { id: 9, lbl: "KitchenAid" },
        { id: 10, lbl: "Whirlpool" },
      ],
      selectBrand: "",
    };
  },

  computed: {
    sliderMin: {
      get: function () {
        let val = parseInt(this.minAngle);
        return val;
      },

      set: function (val) {
        val = parseInt(val);
        if (val > this.maxAngle) {
          this.maxAngle = val;
        }
        this.minAngle = val;
      },
    },

    sliderMax: {
      get: function () {
        let val = parseInt(this.maxAngle);
        return val;
      },

      set: function (val) {
        val = parseInt(val);
        if (val < this.minAngle) {
          this.minAngle = val;
        }
        this.maxAngle = val;
      },
    },
  },

  methods: {
    filterRangePrice() {
      this.$emit("filter-price", this.selectPrice);
    },
  },
};
</script>

<style scoped>
.sidebar {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  max-height: 60%;
}

.sidebar .filter-heading {
  position: absolute;
  top: 177px;
  left: 290px;
  line-height: 1.2;
  color: var(--primary-text-color);
  font-weight: 500;
  font-size: 14px;
  letter-spacing: 0.6px;
}

.sidebar-body {
  width: 260px;
  position: absolute;
  left: 285px;
  top: 219px;
  margin-left: 5px;
  padding: 21px;

  color: var(--primary-text-color);
  background-color: var(--bg-white);
  box-shadow: 0 4px 24px 0 rgb(34 41 47 / 10%);
  border-radius: 5px;
}

.sidebar-body .filter-title {
  display: flex;
  font-weight: 500;
  font-size: 15px;
}

.multi-range,
.product-categries,
.brands {
  display: flex;
  margin-top: 17px;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}

.multi-range-group,
.product-categries-group,
.brands-group {
  display: flex;
  justify-content: flex-start;
}

.multi-range-group label,
.product-categries-group label,
.brands-group label {
  font-size: 14px;
  font-weight: 400;
  padding-bottom: 12px;
  margin-left: 20px;
}

input[type="radio"]:focus {
  outline: none;
}

.custom-control-input {
  position: absolute;
  left: 20px;
  width: 1rem;
  height: 1.225rem;
}

.price-range {
  margin-top: 20px;
  display: flex;
  align-items: center;
}

.price-title {
  font-weight: 500;
  font-size: 15px;
  /* margin-bottom: 1.3rem;
  margin-top: 0.3rem; */
}

.price-range {
  margin-top: 20px;
  display: flex;
  align-items: center;
}

.price-title {
  font-weight: 500;
  font-size: 15px;
  text-align: left;
  margin-bottom: 1rem;
  margin-top: 1.7rem;
}

.slidecontainer {
  position: absolute;
  right: 20px;
}

.range-slider {
  width: 220px;
  text-align: center;
  position: relative;
  padding: 7px 0px;
}

.range-slider input[type="range"] {
  position: absolute;
  left: 0;
  bottom: 0;
}

input[type="range"] {
  -webkit-appearance: none;
  width: 100%;
}

input[type="range"]:focus {
  outline: none;
}

input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 5px;
  cursor: pointer;
  background: var(--badge);
  border-radius: 10px;
  box-shadow: none;
}

input[type="range"]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  height: 15px;
  width: 15px;
  margin-top: -5px;
  border: 2px solid var(--badge);
  border-radius: 50%;
  background: var(--bg-light);
  cursor: pointer;
  -webkit-appearance: none; /*to empty out the circles*/
}

.slider {
  -webkit-appearance: none;
  appearance: none;
  width: 90%;
  height: 5px;
  margin-top: 55px;
  background: #d3d3d3;
  outline: none;
  border-radius: 8px;
  opacity: 0.7;
  -webkit-transition: 0.2s;
  transition: opacity 0.2s;
}

.slider:hover {
  opacity: 1;
}

.categories-title {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  font-weight: 500;
  font-size: 15px;
  margin-top: 50px;
}

.brands-title,
.rating-title {
  display: flex;
  font-weight: 500;
  font-size: 15px;
  margin-top: 22px;
}

.rating-list {
  display: flex;
  justify-content: flex-start;
}

.rating-list-items {
  list-style: none;
  margin-top: 12px;
}

.rating-list-items a {
  text-decoration: none;
  color: #ff9f43;
  font-size: 14px;
}

span.and-up {
  color: var(--badge);
  font-size: 14px;
  text-transform: lowercase;
  position: absolute;
  padding: 4px;
}

span.rating-mount {
  position: absolute;
  right: 14px;
  font-size: 14px;
  padding: 5px 3px;
}
</style>
