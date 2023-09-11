<template>

  <div class="home">
    <div class="feature-card">
        <div class="title" style="padding:10px;">
          <v-img
            :aspect-ratio="10/4"
            src="../assets/Dilo.jpg"
            :class="img"
            style="float:right;margin-right:2px;margin-top:1px;width:50px;height:50px;background-color:white; border-radius:50%;border:1px solid white;"
          ></v-img>

          <h1 style='text-align:center;'>Movie App</h1>
        </div>
      <router-link to="/movies/f23323j">

        <v-img
            :aspect-ratio="10/4"
            
            src="../assets/movies-img.jpg"
            :class="img"
            style="width:100%;"
          ></v-img>

        <div class="details">
          <h3>Vue App movie</h3>
          <p>This is movie app which will be integrated with movie api colled omdbapi , it's designed by BIKMAN DJUMA</p>
        </div>

      </router-link>
    </div>
    
    <div id="error" style="display:none;color:red;text-align:center;">Search field is required !</div>

    <form @submit.prevent="SearchMovies()" class="search-box">
        <input type="text" placeholder="Search movie . . . . . " v-model.trim.lazy="search" id="myInputSearch">
        <button type="submit">
          <v-icon>mdi-magnify</v-icon>
        </button>
    </form>
  
  </div>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.omdbID">
        <router-link :to="'/movie/'+movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="movie image"/>
            <div class="type">{{movie.Type}}</div>
          </div>
          <div class="detail">
              <p class="year">{{movie.Year}}</p>
              <h3>{{movie.Title}}</h3>
          </div>
        </router-link>
      </div>  
    </div>

</template>

<script>
  import { ref } from 'vue';
  import env from '@/env.js';
    export default{

     data(){
        return{
          img:'images',
          items: ['foo', 'bar', 'fizz', 'buzz'],
          files: [],
        }
     },

     setup() {
        const search=ref("");
        const movies=ref([]);
        
        const SearchMovies = () => {
            if(search.value == ""){
                document.getElementById('error').style.display='block';
            }else{
                fetch(`http://www.omdbapi.com/?s=${search.value}&apikey=${env.apikey}`)
                  .then(response => response.json())
                  .then(data => {
                    movies.value = data.Search;
                    search.value="";
                    //console.log(data);
                });

                document.getElementById('error').style.display="none";
                document.getElementById('myInputSearch').value="";
            }
        } 

         return {
            search,
            movies,
            SearchMovies,
         }   

     }
    
  }
</script>

<style lang="scss">

  .feature-card{
      position:relative;

    .title{
      background-color:steelblue;
      color:white;
    }

    @media(max-width:900px){
      .images{
        position:absolute;
        margin-top:-14px;
      }
    }

    .images{
        position:relative;
        display:block;
        width:100%;
        height:300px;
        object-fit:cover;
        z-index:0;
    }

    a{
      text-decoration:none;
    }

    .details{
        position:absolute;
        left:0;
        right:0;
        bottom:0;
        background-color:rgb(0,0,0,0.6);
        padding:16px;
        z-index:1;

        h3{
          color:white;
          text-align:center;
          margin-bottom:16px;
        }

        p{
          color:white;
          text-align:center;
        }
    }

  }

  form{
      display:flex;
      max-width:480px;
      margin:0 auto 1.5rem;
  }

   button{
          margin-top:-57px;
          margin-left:260px;          
          font-size:20px;
          color:white;
          background-color:#42B883;
          border-radius:8px;
          text-transform:uppercase;
          transition:0.4s;
          border:none;
          background:none;
          outline:none;

          .img-submit{
              max-width:40px;
              max-height:40px;
          }

          .img-submit:hover{
            cursor:pointer;
          }

    }

  .search-box{
      display:flex;
      flex-direction:column;
      justify-content:center;
      align-items:center;
      padding:16px;

      input{
        display:block;
        border:none;
        outline:none;
        appearance:none;
        background:none;

        &[type="text"]{
          width:300px;
          color:white;
          background-color:#496583;
          border-radius:8px;
          padding:10px 16px;
          font-size:20px;
          transition:0.4s;
          margin-bottom:15px;

          &::placeholder{
            color:white;
          }

          &:focus{
            box-shadow:0px 3px 6px rgb(0,0,0,0.4);
          }
        
        }

      }

  }   


      .movies-list{
          display:flex;
          flex-wrap:wrap;
          margin:0px 8px;

          .movie{
              max-width:260px;
              flex: 1 1 50%;
              padding:16px 8px;

              .movie-link{
                  display:flex;
                  flex-direction:column;
                  height:100%;

                  .product-image{
                      position:relative;
                      display:block;

                      img{
                          display:block;
                          width:100%;
                          height:275px;
                          object-fit:cover;
                      }

                      .type{
                          position:relative;
                          padding:8px 16px;
                          background-color:#42BB83;
                          color:#FFF;
                          bottom:16px;
                          left:0px;
                          text-transform:capitalize
                      }
                  }

                  .detail{
                    margin-top:-30px;
                    background-color:gray;
                    padding:16px 8px;
                    flex: 1 1 100%;
                    border-radius:0px 0px 8px 8px;

                    .year{
                      color:white;
                      font-size:14px;
                    }

                    h3{
                      color:#FFF;
                      font-weight:600;
                      font-size:17px;
                    }
                  }
              }
          }
      }

      
      footer{
          margin-bottom:0px;
      }

</style>
