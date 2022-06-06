<template>
  <footer class="footer">
    <p class="left">
      COPYRIGHT © 2022 <a href="#" class="owner">Pixinvent</a>,
      <span class="reserved">All rights Reserved</span>
    </p>
    <p class="right">
      Hand-crafted & Made with
      <span class="material-icons-outlined"> favorite_border </span>
    </p>
  </footer>
</template>

<script>
export default {
  name: "Footer-component",
};
</script>

<style scoped>
.footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-left: 260px;
  padding: 0.8rem 2rem;
  min-height: 3.35rem;
  color: var(--primary-text-color);
  font-size: 14px;
  word-spacing: 0.7px;
}

.footer p.left {
  margin-top: 0.25rem;
  text-align: left;
}
.left a {
  color: var(--badge);
  text-decoration: none;
  margin-left: 4px;
}

.footer p.right {
  display: flex;
  align-items: center;
  margin-top: 0.25rem;
}

.right span {
  color: #ea5455;
  position: relative;
  top: 0;
  left: 5px;
  height: 1.51rem;
  width: 1.51rem;
  font-size: 1.51rem;
}
</style>
