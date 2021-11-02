<template>
	
	<transition name="modal_on_off">
		<Modal @modal_close="modal_on = false" :modal_on="modal_on" :room="원룸들[누른거]"/>
	</transition>
    <div class="menu">
        <a v-for="(menu, i) in 메뉴들" :key="i">{{menu}}</a>
    </div>
	<Discount />
	<button class="price btn1" @click="sortBack">- 기본순</button>
	<button class="price btn2" @click="rowPrice">- 낮은가격순</button>
	<button class="price btn3" @click="highPrice">- 높은가격순</button>
	<Card @modal_open="누른거 = i; modal_on = true; " :room="원룸들[i]" v-for="(room , i) in 원룸들" :key="i"/>
	
</template>

<script>
import data from './assets/oneroom.js'
import Card from "./components/Card.vue";
import Modal from "./components/Modal.vue";
import Discount from "./components/Discount.vue";

export default {
    name: 'App',
    data(){
        return{
			원본데이터 : [...data],
			누른거 : 0,
            원룸들 : data,
            modal_on : false,
            메뉴들 : ['Home', 'Shop', 'About'],
        }
    },
    methods : {
        inc() {
            this.num += 1;
        },
        close(){
            this.modal_on = false;
        },
		sortBack(){
			this.원룸들 = [...this.원본데이터];
		},
		rowPrice() {
			this.원룸들.sort(function(a,b) {
				return a.price - b.price;
			});
		},
		highPrice(){
			this.원룸들.sort(function(a,b){
				return b.price - a.price;
			});
		},
		
    },
    components: {
		Card : Card,
		Modal : Modal,
		Discount : Discount,

    }
}
</script>

<style>








.box{border-radius: 6px;}
.box img{border-radius: 5px;;}

.price{margin-right: 5px; margin-top: 10px; border-radius: 5px; border:1px solid lightgray; padding: 5px; background-color: #fff; cursor: pointer; font-weight: bold;}
h4{cursor: pointer;}

.close{
    position: absolute; right: 10px; top: 10px; cursor: pointer; font-weight: bold;
    border: none; color: #fff; background-color: black; padding: 5px; border-radius: 5px; font-size: 10px;
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}
.box{
    border: 1px solid #ddd; margin-top: 10px;
	margin-bottom: 50px;
    
}
.menu {
    background-color: gray;
    padding: 15px;
    border-radius: 5px;
}
.menu a{
    color: #fff;
    padding: 10px;
}
.room_img{
    width: 100%;
}

div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed; top: 0%; left: 0%; 
  padding: 20px;
}
.white-bg {
    border-radius: 10px;
    background-color: #fff;
    width: 90%;
    position: fixed; top: 50%; left: 50%; transform: translate(-50%,-50%);
    /* padding: 20px;	 */

}
.white-bg img{width: 100%; border-radius: 10px; padding: 5px; box-sizing: border-box;}
.discount{
	margin-top: 10px;
	background-color: antiquewhite; border-radius: 5px;
	padding: 1px;
	font-size: 20px; font-weight: bold; 
	
}

.modal_on_off-enter-from{opacity: 0;}
.modal_on_off-enter-active{ transition: all 0.5s;}
.modal_on_off-enter-to{opacity: 1;}
.modal_on_off-leave-from {transform: translateY(-50%); transition: all 0.5s;}
.modal_on_off-leave-active{ transition: all 0.5s;}
.modal_on_off-leave-to {transform: translateY(-1100px); transition: all 0.5s;}
</style>
