<template>
  <p class="copyright">
    This game owned by Leekyoung9x -
    <a href="https://www.facebook.com/profile.php?id=100079545935405"
      >view here</a
    >
  </p>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "../assets/style/globall.scss";

.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: $light-color;
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}
</style>
