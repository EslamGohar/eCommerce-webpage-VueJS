<template>
  <!-- grid view layout -->
  <div class="grid-view" v-if="isGridView">
    <div class="card">
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

  <!-- list view layout -->
  <div class="list-view" v-if="!isGridView">
    <div class="box">
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
</template>

<script>
export default {
  name: "ProductCard",
  props: ["prod"],
};
</script>

<style scoped>
.grid-view {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 20px;
  grid-row-gap: 10px;
  position: relative;
  left: 276px;
  bottom: 12px;
  margin: 295px;
  /*
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-start;
  */
}

.list-view {
  /* display: block;
  position: relative;
  left: 276px;
  bottom: 12px;
  margin: 295px; */

  display: flex;
  position: relative;
  left: 276px;
  top: 272px;
  margin: 30px 298px;
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
  transform: scale(1.03);
  box-shadow: 0 2px 8px 2px rgb(34 41 47 / 30%);
}

.card-body .product-image {
  width: 220px;
  padding: 25px 0;
}

.card-body .item-rating ul {
  list-style-type: none;
  display: flex;
  justify-content: flex-start;
}

.card-body .item-rating span {
  font-size: 19px;
  color: #ff9f43;
  margin-left: 5px;
}

.card-body .item-details .item-title {
  padding-top: 10px;
  padding-bottom: 10px;
  margin-top: -15px;
  margin-left: 11px;
  font-weight: 600;
  font-size: 14px;
  text-align: left;
  text-transform: capitalize;
  color: var(--primary-text-color);
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.item-title:hover {
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

/****** List view layout ******/

.box {
  display: flex;
  overflow: hidden;
  height: 210px;
  background-color: var(--bg-white);
  border-radius: 6px;
  transition: 0.3s all ease-in-out;
}

.box:hover {
  transform: scale(1.03);
  box-shadow: 0 2px 8px 2px rgb(34 41 47 / 30%);
}

.box .prod-image {
  display: flex;
}

.box .prod-image img {
  padding: 38px 0;
  width: 187px;
}

.box-body {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  padding: 10px 15px;
  border-right: 1px solid #ebe9f1;
}

.box-body .prod-name {
  padding-top: 10px;
  padding-bottom: 10px;
  font-size: 14px;
  font-weight: 600;
  color: var(--primary-text-color);
  text-align: left;
  text-transform: capitalize;
}

.box-body .company {
  margin: 0.3rem 0 0.5rem;
  font-size: 12.5px;
  text-transform: capitalize;
}

.box-body .prod-brand {
  font-weight: 600;
  color: #7367f0;
  text-decoration: none;
}

.box-body .prod-description {
  text-align: left;
  overflow: hidden;
  text-overflow: ellipsis;
  font-size: 12px;
  letter-spacing: 0.4px;
  line-height: 19px;
  color: var(--primary-text-color);
  width: 343px;
}

.box-options {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 190px;
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
  color: #7367f0;
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
  box-shadow: 0 5px 15px 0 rgb(79 69 190 / 40%);
}
</style>
