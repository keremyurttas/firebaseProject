<template>
  <div class="bg-red-500">
    <div class="form">
      <input v-model="userName" type="text">
    </div>
    <button class="save">
      save
    </button>
  </div>
</template>
<script>
 export default{
  data(){
    return{
      userName:"",
    }
  },
  methods:{
    save(){
      alert(this.userName)
    }
  }
 }
</script>
<style>

</style>