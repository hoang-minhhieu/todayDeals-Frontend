<template>
  <div class="hello">
    <h1>Happy counting!</h1>
    <p style="font-size:40px">{{count}} </p>
  </div>
</template>

<script lang="ts">
import axios from 'axios'
export default {
  data: ()=> {
   return{ count:0
   }
  },
  mounted:  async function () {
    console.log("Created");
    console.log(import.meta.env)

    await this.loadCount();
  },
  methods:{
    loadCount:  async function () {
      let result= await axios.get(`${import.meta.env.VITE_APP_APIURL}count`);
      this.count=result.data.changed;
      setTimeout(this.loadCount,3000);
    }
  }
}
</script>