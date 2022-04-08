<template>

    <main>
        
     <div class="all" >
    
            <div class="clearfix" v-for="lesson in lessonsinfo" :key="lesson.id">
                <div class="border">
               <figure>
                <img v-bind:src="lesson.image">
               </figure>
                <p v-text="lesson.subject"></p>
                <p v-text="lesson.Location"></p>
                <p>Price:{{lesson.Price}}</p>
                <p>Spaces:{{lesson.Spaces}}</p>
                <button class="button" @click="addLesson(lesson)" v-if='canAddToCart(lesson)' >Add to Cart</button>
                <button class="buttonDisabled" disabled='disabled' v-else >Add to Cart</button>
                </div>
            </div>
            </div>
    </main>
</template>

<script>


export default {
  name: "lessonsPage",
 props: ['lessonsinfo'],
 data() {
  return{
    image:"",
    subject:"",
    location:"",
    Price:"",
    Spaces:"",
    cart: []
  };
  
},
// mounted(){
//     fetch('https://coursework2-proj.herokuapp.com/collection/Lesson%20Information')
//     .then(res => res.json())
//     .then(data => this.lessonsinfo = data)
//     .catch(err => console.log(err.message))
// },


            methods:{
                 
                    addLesson(lesson) {
                        console.log("added lesson", lesson.id)
                        this.$emit('addLesson',lesson)
                //     if(lesson.Spaces > 0){
                //        lesson.Spaces = lesson.Spaces -1; //Reduce slots available once added
                //    }
                },
                canAddToCart(lesson){
                    return lesson.Spaces > this.cartCount(lesson.id);
                },
                cartCount(id) {
                    let count = 0;
                    for (let i = 0; i < this.cart.length; i++) {
                        if (this.cart[i] === id) {
                            count++;
                        }
                    }
                    return count;
                }
},
//   computed:{
//     cartItemCount: function(){
//      return this.cart.length || '' ;
//     }
//   }
}


</script>

<style>

</style>


