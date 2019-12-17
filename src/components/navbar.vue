<template>
 
    <nav class="navbar navbar-expand-sm fixed-top navbar-light bg-white">
      <a class="navbar-brand" href="#"><span><img alt="Vue logo"  src="../assets/logo.png" /></span></a>
      <button
        class="navbar-toggler d-lg-none"
        type="button"
        data-toggle="collapse"
        data-target="#collapsibleNavId"
        aria-controls="collapsibleNavId"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button> 

      <form class="form-inline my-2 my-lg-0 " style="margin: 0 auto;">
        <!-- Actual search box -->
        <div class="has-search">
          <i class="fa fa-search form-control-feedback"></i>
          <input type="text" class="form-control" placeholder="Search" v-model="filterSearch" @keyup="search()" />
        </div>
      </form>
       <div class="collapse navbar-collapse" id="collapsibleNavId">
        <ul class="navbar-nav ml-auto mt-2 mt-lg-0">
          <li class="nav-item" v-for="navbaritem in navbaritems" :key="navbaritem.id">
              <router-link class="nav-link" :to="navbaritem.link" >{{navbaritem.label}}</router-link> 
          </li>
        </ul>
      </div>
    </nav>
  
</template>

<script>
import axios from "axios";
    export default {
        
        name: "navbar",
        props: {
            msg: String
        },
        data () {
            return {
                navbaritems: [],
                filterSearch:[],
                errors: []
            }
        },
         mounted () {
            axios.get(`http://localhost/json.php`).then(response => {
                // JSON responses are automatically parsed.
                if (response.data.length) {
                    this.navbaritems = response.data;
                } else {
                    alert("No Data Found");
                }
                            
            }).catch(e => {
            this.errors.push(e);
            })
         },
         
         methods: {
          search() {   
              this.$root.$emit('SearchValue',  this.filterSearch);
          }
       }
       
    };


   

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped >
   

   img {
    width: 45px;
    vertical-align: middle;
    border-style: none;
    height: 45px;
    }
    
    .has-search .form-control {
        padding-left: 2.375rem;
        -webkit-box-shadow: 0px 2px 4px 1px rgba(0, 0, 0, 0.1);
        -moz-box-shadow: 0px 2px 4px 1px rgba(0, 0, 0, 0.1);
        box-shadow: 0px 2px 4px 1px rgba(0, 0, 0, 0.1);
        width: auto;
        transition: width 1s;
        border: none;
    }

  
    .has-search .form-control:hover,
    .has-search .form-control:focus,
    .has-search .form-control:active {
        width: 100%;
    }

    .has-search .form-control-feedback {
        position: absolute;
        z-index: 2;
        display: block;
        width: 1.375rem;
        height: 2.375rem;
        line-height: 2.375rem;
        text-align: center;
        pointer-events: none;
        color: #aaa;
        padding-left: 5px;
    }

    .navbar-brand span {
        font-size: 22px;
        color: #b70101;
    }

  .navbar-light .navbar-nav .nav-link:focus, .navbar-light .navbar-nav .nav-link:hover {
    color: rgba(0,0,0,.7);
    border-bottom: 3px solid;
}

    .navbar .nav-item .nav-link {
        text-transform: uppercase;
        color: #000;
        font-family: fantasy;
        font-size: larger;
        border-bottom: 3px solid #ffffff;
    }
   
  


</style>
