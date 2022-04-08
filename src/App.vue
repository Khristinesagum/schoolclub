<template>
  <div id="app">
    <header>
    <h1 class="sitename" v-text="sitename"></h1>
            <h1 class="sitename" v-text="sitename"></h1>
           
            <button class="shoppingCart" v-on:click='showShoppingCart' v-if="this.cart.length > 0" >
                {{this.cart.length}}
                <span class="fas fa-cart-plus"> </span>Shopping cart
            </button>
            <button class="shoppingCartDisabled" disabled="disabled" v-else >
                <span class="fas fa-cart-plus"> </span>Shopping cart
            </button>
            <!-- <p class="search">
                <input class="searchText" id="input" v-model="search" placeholder="search..." type="text"/>
            </p> -->
    </header><br>
    <main>
      <div v-if="showLessons">
<lessons-page :lessonsinfo='lessonsinfo' @addLesson='addToCart'></lessons-page>
      </div>
    <div v-else>
      <button class="previousButton" @click="previousPage()">Go to lessons</button>
 <checkout-page :cart="cart" @removeItemFromCart='removeLesson'></checkout-page>
    </div>
   
    </main>
     <!-- <component v-bind:is="component" /> -->
  </div>
</template>

<script>  
// const lessonsPage =() => import ('./components/lessonsPage.vue')
// const checkoutPage =() => import ('./components/checkoutPage.vue')
// import lessonsPage from './components/lessonsPage.vue'
// import checkoutPage from './components/checkoutPage.vue'
const lessonsPage = function() {
  return import('./components/lessonsPage.vue')
}
const checkoutPage = function() {
  return import('./components/checkoutPage.vue')
}
export default {
  name: 'App',
  components: {
     'lessons-page':lessonsPage,
     'checkout-page':checkoutPage
},
 data() {
  return{
    sitename:"School Classes and Activities",
    cart: [],
    lessonsinfo: [],
    showLessons: true,
    inCart: 0
    // currentView: lessonsPage
    // component: "checkoutPage"
  }
  
},
mounted(){
    fetch('https://coursework2-proj.herokuapp.com/collection/Lesson%20Information')
    .then(res => res.json())
    .then(data => this.lessonsinfo = data)
    .catch(err => console.log(err.message))
},
  methods:{
    showShoppingCart(){
      this.showLessons = this.showLessons ? false: true;
                        
    },
    addToCart(lesson){
      this.cart.push(lesson)
      // lesson.Spaces --
      if(lesson.Spaces > 0){
      lesson.Spaces = lesson.Spaces -1; //Reduce slots available once added
      }
    },
    removeLesson(lesson){
      // this.cart.splice(this.cart.indexOf(lesson),1)
      // lesson.Spaces ++
                    if(this.cart.splice(this.cart.indexOf(lesson),1)){
                      //  lesson.Spaces ++
                        lesson.Spaces =lesson.Spaces +1;
                    }
      // this.cart.forEach(item => {
      //   if (item.id === lesson.id){
      //     lesson.Spaces ++
      //     this.cart.splice(this.cart.indexOf(lesson),1)
      //   }
      // })
    },
      previousPage(){
    this.showLessons = this.showLessons ? false: true;
                      
    }
  },
  // computed:{
  //   cartItemCount: function(){
  //    return this.cart.length || '' ;
  //   }
  // }
}

</script>

<style scoped src="./assets/mystyle.css">

</style>
