<template>
  <div>
    <div
      class="number"
      :id="'number-' + number"
      v-for="number in n()"
      :key="number"
      @mouseover="hov(number)"
      @mouseout="reset"
    >
      {{ number }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      limit: this.$parent.limit,
      numbers: []
    };
  },
  watch: {
    ["$parent.limit"](newLimit) {
      this.limit = newLimit;
    }
  },
  methods: {
    n() {
      let numbers = [];
      let currentLimit = Number(this.limit); // Converting string to number to avoid type coercion issues

      for (var i = 1; i <= currentLimit; i++) {
        // 1.There are the configured amount of numbers being displayed but they are ranging from 0. Changed initial value of i=1 so that the numbers start at 1.
        // 2. Set limit to the new currentLimit variable which is now a number and changed the loop to run until i=currentLimit so that the full range of numbers from 1 to the configured number are displayed. By converting currentLimit to a number it would also of allowed me to set i = currentLimit + 1 to achieve the same result. Previously this would have resulted in 1 being appended to the currentLimit and the output would not be what is required.
        numbers = [...numbers, i];
      }
      console.log(numbers);
      return numbers.sort(() => Math.random() - 0.5);
    },
    hov(number) {
      const nums = document.querySelectorAll(".number");
      console.log(number);

      for (let i = 0; i < nums.length; i++) {
        const num = nums[i].textContent.trim();
        if (number % num === 0) {
          nums[i].classList.add("active");
          console.log("divisor", num);
        }
      }
    },
    reset() {
      const nums = document.querySelectorAll(".number");
      nums.forEach(num => num.classList.remove("active"));
    }
  }
};
</script>

<style scoped>
.number {
  display: inline-block;
  padding: 5px;
  background-color: lightgrey;
  /*Added some extra styling for emphasis on hovered number and divisors and to make each number block the same size */
  width: 30px;
  height: auto;
  text-align: center;
  margin: 10px;
  cursor: pointer;
  transition: transform 0.3s ease-out;
}

/*Set hovered number's background to green so it is easier to distinguish what number was hovered over.*/
.number:hover {
  background-color: green;
  transform: scale(1.2); /*Emphasise hovered number */
}

.active {
  background-color: red;
  transform: scale(1.2); /*Emphasise the divisor */
}
</style>
