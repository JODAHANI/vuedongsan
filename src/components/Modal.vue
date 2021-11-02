<template>
	<div class="black-bg" v-if="modal_on == true">
        <div class="white-bg">
			<img :src="room.image">
            <h4>{{room.title}}</h4>
			<!-- <input @input=" month = $event.target.value"> -->
			<input v-model="month">
            <p> {{month}}개월 할부시 => 월 납입금 :{{room.price / parseInt(month)}}만원</p>
            <button class="close" @click="$emit('modal_close')">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
	name : 'Modal',
	data() {
		return {
			month : 1,
		}
	},
	
	props : {
		modal_on : Boolean,
		room : Object,

	},
	watch : {
		month(a,b) {
			if(isNaN(a)){
				alert('숫자만 입력하세요.');
				return this.month = 1;
			}
			if(a >= 13){
				alert('최대 12개월까지 가능합니다.')
				return this.month = b;
			}

		},
	},
	
}
</script>

<style>

</style>