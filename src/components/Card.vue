<template>
	<div class="box">
		<img :src="room.image" class="room_img" >
        <h4 @click="open_modal">{{room.title}}</h4>    
        <p> {{room.price}} 만원</p>
    </div>  
</template>

<script>
export default {
	name : 'Card',
	props : {
		room : Object
	},
	methods : {
		open_modal() {
			this.$emit('modal_open')
		}
		
	}
	
}
</script>

<style>

</style>