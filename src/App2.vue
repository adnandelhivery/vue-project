<!-- options API -->
<script>
export default{
  data(){
    return{
      name:"Adnan Khan",
      status:"active",
      tasks:["Task1","Task2","Task3"],
      link:"https://www.google.com"
    };
  },


methods:{
    toggleStatus(){
      if(this.status === "active"){
        this.status = "pending";
    }
    else if (this.status === "pending"){
      this.status = "inactive";
  } 
   else{
    this.status = "active";
  }
},
},
};


</script>

<template>
  <h1 class="">{{ name }}</h1>
  <p v-if="status === 'active'">User is {{ status }}</p>
  <p v-else-if="status === 'pending'">User is  {{ status }}</p>
  <p v-else>User is {{ status }}</p>

  <h3>Tasks:</h3>
  <ul class="">
    <li v-for="task in tasks":key="task">{{ task }}</li>
  </ul>
<br/>
  <!-- <a v-bind:href="link">Click for Google</a>  v-bind directive -->
  
  <!-- //alternate way to do the same thing -->
  <a :href="link">Click for Google</a> 

  <!-- <button v-on:click="toggleStatus">change status</button> handling event -->
  <button @click="toggleStatus">change status</button>  <!-- alternate way to do the same thing -->
</template>
