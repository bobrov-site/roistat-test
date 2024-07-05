<template>
    <button class="button">
        <slot></slot>
    </button>
</template>

<script>
export default {
  name: 'PrimaryButton',
};
</script>

<style scoped>
.button {
  width: 200px;
  height: 50px;
  border-radius: 10px;
  background-color: #2D9CDB;
  color: #fff;
  font-size: 18px;
  font-weight: 400;
  border: none;
  cursor: pointer;
}
.button:hover {
  background-color: #3DA8F5;
}
</style>
