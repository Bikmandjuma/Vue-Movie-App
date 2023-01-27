<template>

  <div class="home">
    <div class="feature-card">
      <router-link to="/movies/f23323j">
        <img src="../assets/image.png" alt="Vue movie app" class="featured-img">

        <div class="details">
          <h3>Vue App movie</h3>
          <p>This is my second vuejs app which will be integrated with movie api colled omdbapi</p>
        </div>

      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
        <input type="text" placeholder="Search movie's name . . . " v-model.trim.lazy="search">
        <!--img src="../assets/search.png" alt="Submit" class="img-submit"-->
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

        }
     },

     setup() {
        const search=ref("");
        const movies=ref([]);
        
        const SearchMovies = () => {
            if(search.value == ""){
                alert('Search field is required !');
            }else{
                fetch(`http://www.omdbapi.com/?s=${search.value}&apikey=${env.apikey}`)
                  .then(response => response.json())
                  .then(data => {
                    movies.value = data.Search;
                    search.value="";
                    //console.log(data);
                });
            }
        } 

         return {
            search,
            movies,
            SearchMovies

         }   

     }
    
  }
</script>

<style lang="scss">
  .feature-card{
      position:relative;

    .featured-img{
        position:relative;
        display:block;
        width:100%;
        height:300px;
        object-fit:cover;
        z-index:0;
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

        &[type="submit"]{
          margin-top:-60px;
          margin-left:400px;
          width:100%;
          max-width:200px;
          font-size:20px;
          color:white;
          background-color:#42B883;
          border-radius:8px;
          padding:10px 16px;
          text-transform:uppercase;
          transition:0.4s;
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
