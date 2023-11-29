<template>
  <button class="btn">
    <img src="@/assets/images/pen.svg" alt="" />
  </button>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.btn {
  position: fixed;
  bottom: 30px;
  right: 30px;
  border-radius: 16px;
  background: var(
    --m-3-read-only-light-surface-3,
    linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11) 0%,
      rgba(103, 80, 164, 0.11) 100%
    ),
    #fffbfe
  );
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.3),
    0px 4px 8px 3px rgba(0, 0, 0, 0.15);
}
</style>