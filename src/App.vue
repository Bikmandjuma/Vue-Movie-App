<template>
   <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  
  <main>
    <Router-view />
  </main>

</template>

<style lang="scss">
  *{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-famill:'fira sans', sans-serif;
  }

  a{
    text-decoration:none;
  }

  body{
      background-color:#35495E;
    }

  header{
    display:flex;
    align-items:center;
    justify-content:center;
    padding:10px 16px;
    background-color:teal;
    box-shadow:0px 0px 6px rgba(0,0,0,0.7);


  }

  h1{
      color:#FFF;
  }

  span{
    color:#42B883;
  }

</style>
