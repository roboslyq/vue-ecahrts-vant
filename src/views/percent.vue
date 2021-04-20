<template>
  <div class="brokenline">
    <div>
      <NavBar />
    </div>
    <br />
    <Percent />
    <br />
    <Percent />
    <br />
    <Percent />
  </div>
</template>

<script>
import NavBar from "../components/navBar";
import Percent from "../components/percent";
export default {
  components: {
    NavBar,
    Percent
  }
};
</script>