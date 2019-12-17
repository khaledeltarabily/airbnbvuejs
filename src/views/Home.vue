<template>
  <div class="home">
   
    <!-- Sec nav bar -->
    <div class="container-fluid nav-btns">
      <a href="#" class="btn effect01"><span>Dates</span></a>  
      <a href="#" class="btn effect01"><span>Guests</span></a>
      <a href="#" class="btn effect01"><span>Work trip</span></a>
      <a href="#" class="btn effect01"><span>Type of place</span></a>
      <a href="#" class="btn effect01"><span>Price</span></a>
      <a href="#" class="btn effect01"><span>Instant book</span></a>
      <a href="#" class="btn effect01"><span>More filters</span></a>
    </div>

    <section class="top-rated"  ref="section">
      <div class="top-rated-inner mt-5">
        <h3>Top-rated places to stay</h3>
        <p>Explore some of the best-reviewed stays in the world</p>
        <div v-if="!filteredItems.length" class="NoResult">No Result</div>
        
         <transition-group name="list" tag="div"   class="row">
          <div class="col-sm-12 col-md-6 col-lg-3 mt-4 " v-for="(cardInfo, cardInfoIndex) in filteredItems" :key="cardInfoIndex"  ref="card">
            <div class="card custom" style="width: 100%; " >
                      <!-- Slider  -->
                      <div class="slider sliderClass" ref="sliders" >
                        <!-- Image inside slider -->
                        <div  v-for="(cardPhoto, PhotoSliderCardIndex) in cardInfo.photos" :key="PhotoSliderCardIndex" :style="{backgroundImage:`url(${cardPhoto})`}"  :class="{ 'show': PhotoSliderCardIndex === 0 }"></div>
                         <!-- The Arrows -->
                        <i  class="left arrows" @click="leftClickArrowCard(cardInfoIndex)" id="leftArrow" style="z-index:2; position:absolute;"><svg viewBox="0 0 100 100"><path d="M 10,50 L 60,100 L 70,90 L 30,50  L 70,10 L 60,0 Z"></path></svg></i>
                        <i  class="right arrows" @click="rightClickArrowCard(cardInfoIndex)" id="rightArrow" style="z-index:2; position:absolute;"><svg viewBox="0 0 100 100"><path d="M 10,50 L 60,100 L 70,90 L 30,50  L 70,10 L 60,0 Z" transform="translate(100, 100) rotate(180) "></path></svg></i>
                        <!-- Heart icon  -->
                        <i class="right heartIconstyle" @click="showModal= true" style="z-index:2; position:absolute;" ><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" width="20.274px" height="20.273px" viewBox="0 0 168.274 168.273" style="enable-background:new 0 0 168.274 168.273;" xml:space="preserve">
                          <g> <path d="M142.267,16.291C123.67,6.052,99.472,9.164,84.14,23.211C68.795,9.157,44.694,6.04,25.988,16.291   C9.953,25.126,0,42.006,0,60.312C0,65.562,0.855,70.78,2.338,75.24c8.038,36.09,75.627,78.891,78.493,80.699l3.31,2.083   l3.312-2.083c2.861-1.809,70.451-44.615,78.324-80.108c1.65-5.058,2.497-10.27,2.497-15.519   C168.28,42.006,158.33,25.126,142.267,16.291z M153.763,72.527c-5.407,24.323-49.322,57.412-69.623,70.717   c-20.302-13.299-64.244-46.412-69.779-71.316c-1.242-3.791-1.878-7.7-1.878-11.63c0-13.774,7.478-26.442,19.498-33.094   c5.626-3.075,11.962-4.701,18.258-4.701c11.274,0,21.894,4.987,29.13,13.691l4.783,5.767l4.774-5.767   c11.35-13.643,31.651-17.601,47.349-8.99c12.062,6.646,19.54,19.32,19.54,33.094C155.797,64.234,155.164,68.144,153.763,72.527z    M149.562,60.307c0,3.221-0.512,6.463-1.547,9.657c-0.427,1.321-1.645,2.165-2.947,2.165c-0.305,0-0.651-0.046-0.95-0.152   c-1.644-0.53-2.558-2.28-2.009-3.928c0.815-2.569,1.242-5.176,1.242-7.742c0-9.222-5.018-17.71-13.08-22.174   c-3.8-2.095-7.94-3.16-12.227-3.16c-1.742,0-3.105-1.403-3.105-3.118c0-1.717,1.363-3.118,3.105-3.118   c5.353,0,10.497,1.321,15.241,3.958C143.327,38.228,149.562,48.807,149.562,60.307z"/></g> <g></g> <g> </g> <g> </g> <g></g> <g> </g> <g></g> <g> </g> <g></g> <g> </g> <g> </g> <g> </g> <g> </g> <g> </g> <g></g><g></g></svg></i>
                        <!-- Title Bar -->
                        <span class="titleBar"> <p>{{cardInfo.title}}</p></span>
                        <!-- Indicator point -->
                        <ol class="carousel-indicators"  > <li v-for="(cardIndicatorPoint, cardIndicatorPointIndex) in cardInfo.photos" :key="cardIndicatorPointIndex"  @click="goTargetDot($event,cardIndicatorPointIndex,cardInfoIndex)" :data-slide-to="cardIndicatorPointIndex"  :class="{ 'active': cardIndicatorPointIndex === 0 }" ></li>  </ol>
                      </div>
              <div class="card-body p-2">
                  <div class="row">
                      <div class="col-8">
                            <span class="badge badge-danger" v-if="cardInfo.badge">{{cardInfo.badge}}</span>
                            <span class="location" style="margin-left: 5px;">{{cardInfo.countryname}}</span>
                      </div>
                      <div class="col-4 card-star-text">
                            <i class="fa fa-star text-danger"></i>
                            <span class="rate" style="margin-left: 3px;">{{cardInfo.rating}}</span>
                      </div>
                  </div>
                <p class="card-text validtion-paragh">{{cardInfo.description}}</p>
                <span class="price"><b>{{cardInfo.cost}}</b> / night</span>
              </div>
            </div>
          </div>
         </transition-group>
       

      </div>
    </section>
    <!-- <v-pagination  v-model="currentPage" :page-count="pageCount"    :classes="bootstrapPaginationClasses" :labels="paginationAnchorTexts">></v-pagination> -->

    <nav v-if="!isMobile"   aria-label="Page navigation Pagation">
      <ul class="pagination justify-content-center" v-if="hidepagation">
        <li class="page-item" :class="{disabled:isPreviousButtonDisabled}" @click="pageChangeHandle('previous')" >
          <a class="page-link" href="#" tabindex="-1">Previous</a>
        </li>
        <li class="page-item " :class="{active:currentPage== index}" v-for="index in pageCount" :key="index" @click="pageChangeHandle(index)" ><a class="page-link" href="#">{{index}} </a></li>
        <li class="page-item"  :class="{disabled:isNextButtonDisabled}" @click="pageChangeHandle('next')">
          <a class="page-link" href="#">Next</a>
        </li>
      </ul>
    </nav>
    <div v-else  class="row">
      <div class="col text-center">
        <button  v-if="hidepagationMobile"   type="button" class="btn btn-style" @click="callRequest()">Load More</button>
      </div>
   </div>

    <!-- Modal view -->
    <ModalFav v-if="showModal" :status="showModal" @close="receviedValue"  />

  </div>
</template>

<script>
    import axios from "axios";
    import ModalFav from "@/components/modal.vue";
import { watch } from 'fs';
    
    export default {
      
      name: "home",
      static: {
        visibleItemsPerPageCount: 8
      },
      components: {
       ModalFav,
      
      },
      data () {
            return {
                cardInfos: [],
                errors: [],
                filterSearch:[],
                search: '',
                currentPage: 1,
                currentPageMobile:1,
                pageCount: 0,
                hidepagation:false,
                hidepagationMobile:true,
                 bootstrapPaginationClasses: {
                    ul: 'pagination',
                    li: 'page-item',
                    liActive: 'active',
                    liDisable: 'disabled',
                    button: 'page-link'  
                  },
                  paginationAnchorTexts: {
                    prev: 'Previous',
                    next: 'Next',
                  },
                showModal: false
            }
      },

      methods:{
         
        leftClickArrowCard: function(cardIndex) {// Go to previous slide
           var position;
           var size = this.$refs.sliders[cardIndex].querySelectorAll("div").length;
           var sliderCardImage = this.$refs.sliders[cardIndex].querySelectorAll("div");
           var sliderCardDots = this.$refs.sliders[cardIndex].querySelectorAll("li");
           // To remove old image and indicator dot
            for (var i = 0; i <size; i++) {
              if (sliderCardImage[i].className === "show"& sliderCardDots[i].className === "active" ) {
                position=i-1;
                sliderCardImage[i].classList.remove("show");
                sliderCardDots[i].classList.remove("active");
                break;
              }
            }
           if (position < 0) position = size - 1;
           // To add new image  and indicator dot
           sliderCardImage[position].classList.add("show");
           sliderCardDots[position].classList.add("active");
        },

         rightClickArrowCard: function(cardIndex) {// Go to next slide
           var position;
           var size = this.$refs.sliders[cardIndex].querySelectorAll("div").length;
           var sliderCardImage = this.$refs.sliders[cardIndex].querySelectorAll("div");
           var sliderCardDots = this.$refs.sliders[cardIndex].querySelectorAll("li");
           // To remove old image  and indicator dot
           for (var i = 0; i <size; i++) {
              if (sliderCardImage[i].className === "show"& sliderCardDots[i].className === "active") {
                position=i+1;
                sliderCardImage[i].classList.remove("show");
                sliderCardDots[i].classList.remove("active");
                break;
              }
            }
            if (position > size - 1) position = 0;
            //this.$refs.sliders[cardIndex].querySelector("div").classList.remove("show");
            // To add new image  and indicator dot
            sliderCardImage[position].classList.add("show");
            sliderCardDots[position].classList.add("active");
         },

         goTargetDot : function(ev,cardIndicatorPointIndex,cardInfoIndex){// On click Dots Indicator in slider card
           var size = this.$refs.sliders[cardInfoIndex].querySelectorAll("div").length;
           var sliderCardImage = this.$refs.sliders[cardInfoIndex].querySelectorAll("div");
           var sliderCardDots = this.$refs.sliders[cardInfoIndex].querySelectorAll("li");
           // To remove old image  and indicator dot
           for (var i = 0; i <size; i++) {
              if (sliderCardImage[i].className === "show"& sliderCardDots[i].className === "active") {
                sliderCardImage[i].classList.remove("show");
                sliderCardDots[i].classList.remove("active");
                break;
              }
            }
            // To add new image  and indicator dot
             //set new bullet
            ev.target.setAttribute("class","active");
            sliderCardImage[cardIndicatorPointIndex].classList.add("show");
            // sliderCardDots[position].classList.add("active");
          },

         receviedValue(status){ 
           if(status===false){
              this.showModal=status;
           }
         },

          pageChangeHandle(value) {
            switch (value) {
              case 'next':
                 if(this.currentPage<this.pageCount){
                    this.currentPage += 1
                 }
                break
              case 'previous':
                 if(this.currentPage>1){
                   this.currentPage -= 1
                 }
                
                break
              default:
                this.currentPage = value
            }
            axios.get(`http://localhost/cardinfojson.php?page=${this.currentPage}&pageSize=${this.$options.static.visibleItemsPerPageCount}`).then(response => {
              // JSON responses are automatically parsed.
              if (response.data.data.length) {
                this.cardInfos = response.data.data;
                console.log(response.data.data);
                this.pageCount = Math.ceil( response.data.totalItems / this.$options.static.visibleItemsPerPageCount);
                console.log(this.pageCount);
              } else {
                alert("No Data Found");
              }
            }).catch(e => {
                this.errors.push(e);
            })
          },
          callRequest(){
            this.currentPageMobile+=1;
             axios.get(`http://localhost/cardinfojson.php?page=${this.currentPageMobile}&pageSize=${this.$options.static.visibleItemsPerPageCount}`).then(response => {
              // JSON responses are automatically parsed.
              if (response.data.data.length) {
               
                this.cardInfos=this.cardInfos.concat(response.data.data);
               
                this.pageCount = Math.ceil( response.data.totalItems / this.$options.static.visibleItemsPerPageCount);
                console.log(this.currentPageMobile);
                if(this.currentPageMobile== this.pageCount){
                   this.hidepagationMobile=false;
                   console.log(this.pageCount );
                 }
              } else {
                alert("No Data Found");
              }
            }).catch(e => {
                this.errors.push(e);
            })
            
          }
      },


      mounted () {
           
          //Request Get Cards info 
          axios.get(`http://localhost/cardinfojson.php?page=1&pageSize=${
          this.$options.static.visibleItemsPerPageCount}`).then(response => {
          // JSON responses are automatically parsed.
          if (response.data.data.length) {
                  this.cardInfos = response.data.data;
                  console.log(response.data.totalItems);
                  this.pageCount = Math.ceil( response.data.totalItems / this.$options.static.visibleItemsPerPageCount)
          } else {
                  alert("No Data Found");
          }
          
          }).catch(e => {
              this.errors.push(e);
          })
        
         this.$root.$on('SearchValue', (filterSearch) => { //recieve value Search and apply filter in home
               console.log(filterSearch);
               this.search=filterSearch;
                
         })
  
      }, 
     
        computed: {
          filteredItems() {
            return this.cardInfos.filter(cardInfo => {
              return (cardInfo.countryname.toLowerCase().indexOf(this.search.toLowerCase()) > -1 ||cardInfo.description.toLowerCase().indexOf(this.search.toLowerCase()) > -1 )
            })
          },
          
          isPreviousButtonDisabled() {
            return this.currentPage === 1
          },
          
          isNextButtonDisabled() {
            return this.currentPage === this.pageCount
          },
          isMobile() {
              if(/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
                return true
              } else {
                return false
              }
            }
         
        },
        watch:{
          filteredItems() {
            //console.log(this.filteredItems);
             if(this.pageCount!=this.currentPage){
                if(this.filteredItems.length>=8){
                  this.hidepagation=true;
                }else{
                  this.hidepagation=false;
                }
             }
          }

        }
      

    };


</script>

<style scoped >

    .btn-style {
      color: #FFF;
      background: rgba(7, 31, 49, 0.75);
      width: 55%;
      margin-top: 15px;
      margin-bottom: 15px;
      border: none;
    }


    .btn-style:hover,.btn-style:focus {
        color: #FFF;
        background: rgba(113, 123, 131, 0.75);
        border: 1px solid rgba(113, 123, 131, 0.75);
     }


   .NoResult {
    text-align: center;
    font-size: 60px;
    margin-top: 120px;
    font-family: fantasy;
   }

    /* animation cards */
    .list-enter-active, .list-leave-active {
      transition: all 1s;
    }
    .list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
      opacity: 0;
      transform: translateY(30px);
    }

      /* sec nav bar style */
    .nav-btns .btn {
      border: 1px solid #b1b1b1;
      border-radius: 20px;
      font-size: 14px;
      white-space: nowrap;
      margin: auto 2px;
    }

    .nav-btns .btn:hover {
      border: 1px solid #444;
    }
    .nav-btns .btn:first-child {
      margin-left: 5%;
    }

    .nav-btns {
        border-top: 1px solid #ebebeb;
        border-bottom: 1px solid #ebebeb;
        padding: 0.5% 0;
        margin-top: 15.1%;
        position: fixed;
        top: 1%;
        z-index: 1000;
        background-color: white;
        overflow: hidden;
        height: 54px;
        display: flex;
        width: 100%;
        overflow-x: scroll;
        justify-content: space-between;
        flex-direction: row;
    }


    .nav-btns .btn:focus {
      outline: 0;
      background-color: #f9f9f9;
      box-shadow: 0 0 0 0;
    }


    ::-webkit-scrollbar { 
        display: none; 
    }


     /* word under sec nav bar */
    .top-rated .top-rated-inner {
      margin: 1% 5%;
    }

    .mt-5, .my-5 {
        margin-top: 5rem!important;
    }

     /* card style*/
    .custom{
      cursor: pointer;
    }

    .slider ul li {
      padding: 0;
      width: 10px;
      height: 10px;
      border-radius: 50%;
      list-style: none;
      float: left;
      margin: 8px 8px 0;
      cursor: pointer;
      border: 1px solid #fff;
      -moz-transition: .3s;
      -o-transition: .3s;
      -webkit-transition: .3s;
      transition: .3s;
    }

    .slider, 
    .slider > div {
        /* Images default to Center Center. Maybe try 'center top'? */
        background-position: center center;
        display: block;
        width: 100%;
        height: 200px;
        /* height: 100vh; *//* If you want fullscreen */
        position: relative;
        background-size: cover;
        background-repeat: no-repeat;
        background-color: #000;
        overflow: hidden;
        -moz-transition: transform .4s;
        -o-transition: transform .4s;
        -webkit-transition: transform .4s;
        transition: transform .4s;
    }

    .slider > div {
        position: absolute;
    }
   
    /* slider arrows style */
    .slider > i {
      color: #5bbd72;
      position: absolute;
      font-size: 26px;
      margin: 20px;
      top: 35%;
      text-shadow: 0 10px 2px #223422;
      transition: .3s;
      width: 15px;
      padding: 10px 11px;
      background: #fff;
      background: rgba(255, 255, 255, .3);
      cursor: pointer;
      line-height: 0;
      box-sizing: content-box;
      border-radius: 50px;
      z-index: 4;
    }

    /* Slider heart style */
    .heartIconstyle {
      top: 0 !important;
      padding: 6px 12px 6px 8px  !important;
      margin-right: 21px !important;
    }


    .slider > i svg {
        margin-top: 3px;
    }

    .slider > .left {
        left: -100px;
    }
    .slider > .right {
        right: -100px;
    }
    .slider:hover > .left {
        left: 0;
    }
    .slider:hover > .right {
        right: 0;
    }

    .slider > i:hover {
        background:#fff;
        background: rgba(255, 255, 255, .8);
        transform: translateX(-2px);
    }

    .slider > i.right:hover {
        transform: translateX(2px);
    }

    .slider > i.right:active,
    .slider > i.left:active {
        transform: translateY(1px);
    }

    .slider:hover > div {
        transform: scale(1.01);
    }

    .hoverZoomOff:hover > div {
        transform: scale(1);
    }

    .slider > ul {
        position: absolute;
        bottom: 7px;
        left: 50%;
        z-index: 4;
        padding: 0;
        margin: 0;
        transform: translateX(-50%);
    }



    .slider > ul > .showli {
      background-color: #7EC03D;
      -moz-animation: boing .5s forwards;
      -o-animation: boing .5s forwards;
      -webkit-animation: boing .5s forwards;
      animation: boing .5s forwards;
    }

    .slider > ul > li:hover {
        background-color: #7EC03D;
    }

    .hideDots > ul {
          display: none;
      }

    .showArrows > .left {
        left: 0;
    }

    .showArrows > .right {
        right: 0;
    }

    .slider > .show {
      z-index: 1;
    }


    .titleBar {
        z-index: 2;
        display: inline-block;
        background: rgba(0,0,0,.5);
        position: absolute;
        width: 100%;
        bottom: 0;
        transform: translateY(100%);
        padding: 0px 0px;
        transition: .3s;
        color: #fff;
    }

    .titleBar * {
        transform: translate(-20px, 20px);
        transition: all 700ms cubic-bezier(0.37, 0.31, 0.2, 0.85) 200ms;
        opacity: 0;
        margin-top: -2px;
    }

    .titleBarTop .titleBar * {
        transform: translate(-20px, -30px);
    }

    .slider:hover .titleBar,
    .slider:hover .titleBar * {
        transform: translate(0);
        opacity: 1;   
        text-align: center;
    }

    /* paraghraph validtion in card*/
    .validtion-paragh{
      text-overflow: ellipsis;
        overflow: hidden;
        margin-top: 0;
        height: 1.2em;
        white-space: nowrap;
        margin-bottom: 1rem;
    }


    /* style indicator point */
    .carousel-indicators li {
      width: 8px;
      height: 8px;
      border:1px solid white;
      border-radius:50%;
      background:rgba(0,0,0,0);
      color:white;
      text-align:center;
      margin-left: 5px;
      margin-right: 5px;
      opacity: 1;
    }


    .carousel-indicators li:hover {
      background-color: #7EC03D;
    }


    .carousel-indicators .active {
      background-color: #7EC03D;
      -moz-animation: boing .5s forwards;
      -o-animation: boing .5s forwards;
      -webkit-animation: boing .5s forwards;
      animation: boing .5s forwards;
    }

    .carousel-indicators {
      bottom: -10px;
    }


    @keyframes boing {
      0% {
          transform: scale(1.2);
      }
      40% {
          transform: scale(.6);
      }
      60% {
          transform: scale(1.2);
      }
      80% {
          transform: scale(.8);
      }
      100% {
          transform: scale(1);
      }
    }


        /* ipad pro sec nav */
    @media (min-width: 992px) and (max-width: 1025px){ 
      .nav-btns {
        border-top: 1px solid #ebebeb;
        border-bottom: 1px solid #ebebeb;
        padding: 0.5% 0;
        margin-top: 6.4%;
        position: fixed;
        top: 0%;
        z-index: 1000;
        background-color: white;
        height: 50px;
        display: inline;
      }

      .nav-btns .btn {
        border: 1px solid #b1b1b1;
        border-radius: 20px;
        font-size: 14px;
      }  

      .slider ul  li {
        padding: 0;
        width: 10px;
        height: 10px;
        border-radius: 50%;
        list-style: none;
        float: left;
        margin: 8px 5px 0;
        cursor: pointer;
        border: 1px solid #fff;
        -moz-transition: .3s;
        -o-transition: .3s;
        -webkit-transition: .3s;
        transition: .3s;
    }

    }


    /* destop sec nav bar */
    @media (min-width: 1200px) {  
      .nav-btns {
        border-top: 1px solid #ebebeb;
        border-bottom: 1px solid #ebebeb;
        padding: 0.5% 0;
        margin-top: 4.8%;
        position: fixed;
        top: 0.8%;
        z-index: 1000;
        background-color: white;
        height: 50px;
        display: inline;
      }

      .nav-btns .btn {
        border: 1px solid #b1b1b1;
        border-radius: 20px;
        font-size: 14px;
      }


        /* -------------------------------new style for sec nav item tags---------------------- */
        /*btn_background*/
        .effect01 {
          color: #FFF;
          border: 4px solid #000;
          box-shadow:0px 0px 0px 1px #000 inset;
          background-color: #000;
          overflow: hidden;
          position: relative;
          transition: all 0.3s ease-in-out;
        }
        .effect01:hover {
          border: 4px solid #666;
          background-color: #FFF;
          box-shadow:0px 0px 0px 4px #EEE inset;
        }

        /*btn_text*/
        .effect01 span {
          transition: all 0.2s ease-out;
          z-index: 2;
        }
        .effect01:hover span,
        .effect01:focus span{
          letter-spacing: 0.13em;
          color: #333;
        }


        /*highlight*/
        .effect01:after {
          background: #FFF;
          border: 0px solid #000;
          content: "";
          height: 155px;
          left: -75px;
          opacity: .8;
          position: absolute;
          top: -50px;
          -webkit-transform: rotate(35deg);
                  transform: rotate(35deg);
          width: 50px;
          transition: all 1s cubic-bezier(0.075, 0.82, 0.165, 1);/*easeOutCirc*/
          z-index: 1;
        }
        .effect01:hover:after {
          background: #FFF;
          border: 20px solid #000;
          opacity: 0;
          left: 120%;
          -webkit-transform: rotate(40deg);
                  transform: rotate(40deg);
        }



    }

        /* tablet style sec nav */
    @media (width: 768px) { 
      .nav-btns {
      border-top: 1px solid #ebebeb;
      border-bottom: 1px solid #ebebeb;
      padding: 0.5% 0;
      margin-top: 13.3%;
      position: fixed;
      top: 0%;
      z-index: 1000;
      background-color: white;
      height: 50px;
      display: inline;
      }

      .nav-btns .btn {
        border: 1px solid #b1b1b1;
        border-radius: 20px;
        font-size: 14px;
      } 
    }

  

        /* phones */
@media (max-width: 575.98px)  { 
      
      
      .nav-btns .btn {
        border: 1px solid #b1b1b1;
        border-radius: 20px;
        font-size: 14px;
        white-space: nowrap;
        margin: auto 2px;
      }

    

      .nav-btns {
        border-top: 1px solid #ebebeb;
        border-bottom: 1px solid #ebebeb;
        padding: 0.5% 0;
        margin-top: 15.1%;
        position: fixed;
        top: 1%;
        z-index: 1000;
        background-color: white;
        overflow: hidden;
        height: 54px;
        display: flex;
        width: 100%;
        overflow-x: scroll;
        justify-content: space-between;
        flex-direction: row;
        }
      
    }
        
</style>