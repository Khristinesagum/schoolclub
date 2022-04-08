<template>
    <main>
         <h3 style="margin-left: 3%;">Shopping cart</h3>
         <!-- <button class="previousButton" @click="previousPage">Go to lessons</button> -->
        <div class="all">
            <div class="clearfix" v-for="(lesson, index) in cart" :key="index">
                <!-- <div class="clearfix" v-for="lesson in cart" :key="lesson.id"> -->
                <div class="border">    
               <figure>
                <img v-bind:src="lesson.image">
               </figure>
                <p v-text="lesson.subject"></p>
                <p v-text="lesson.Location"></p>
                <p>Price:{{lesson.Price}}</p>
                <button class="button" @click='removeItemFromCart(lesson)'>Remove item</button>
                </div>
            </div>
            </div>
        <div class="checkoutPage">
                <h2>Checkout Page</h2>
                <p>
                    <strong>Name:</strong>  
                    <input class="textfield" v-model="FullName" value="" name="" onkeypress="onlyLetters(event)" type="text" />
                </p>
                <p>
                    <strong>Phone:</strong>
                    <input class="textfield" v-model.number="PhoneNumber" value="" onkeypress="onlyNumbers(event)"/>
                </p>
                <!-- <button class="buttonCheckout"  >Checkout</button> -->
                                <button class="buttonCheckout"  v-on:click="submitForm"  >Checkout</button>
            </div>
    </main>
</template>

<script>

export default {
  name: "checkoutPage",
 props: ['cart'],
 data() {
  return{
    Fullname:"",
    PhoneNumber:"",
  };
  
},
methods :{
    removeItemFromCart(lesson){
    this.$emit('removeItemFromCart',lesson)
                        
    },
     submitForm(){
                    alert('Order has been submitted');
                }
}
}

</script>