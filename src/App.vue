<template>
  <div id="app">
    <!-- Set min of input to 0 to prevent arrow controlled decrement from going into negatives --><!-- Set min of input to 0 to prevent arrow controlled decrement from going into negatives -->
    <!-- Added @focus to select the text when the input is focussed so the user can just type a new number without have to delete the current one first -->
    <!-- Added v-on:input="cleanNum()" to remove possible negatives or decimals  -->
    <input
      type="number"
      min="0"
      v-model="limit"
      v-on:input="cleanNum()"
      @focus="$event.target.select()"
    />
    <Numbers />
  </div>
</template>

<script>
import Numbers from "@/components/Numbers";

export default {
  name: "App",
  components: { Numbers },
  data() {
    return {
      limit: 100
    };
  },
  //Method cleanNum: added to remove negatives and decimals
  methods: {
    cleanNum: function() {
      var inputNum = this.limit;
      inputNum = inputNum.replace(/[^\d]/g, "");
      if (inputNum.indexOf(".") < 0 && inputNum != "") {
        inputNum = parseInt(inputNum);
      }
      this.limit = inputNum;
    }
  }
};
</script>

<style scoped></style>
