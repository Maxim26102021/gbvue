<template>
  <div class='wrapper'>
    <button @click='$emit("press-num", num)' v-for='(num, indx) in nums' class='wrapper__numbers' :key='indx'>{{ num }}</button>
  </div>
</template>

<script>
export default {
  name: 'Numbers',
  data() {
    return {
      nums: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    };
  }
};
</script>

<style>
.wrapper {
  display: flex;
}
.wrapper__numbers {
  width: 50px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>