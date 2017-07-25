<template>
<li style="list-style-type:none;" v-if="willShow">
	<div class="content">
		<label class="item-label item-checkbox" >
	    	<input class="item-radio" type="checkbox" @click="itemComplete" >
       		<span class="item-radioInput"></span>
    	</label>
		<label :class="isSelected ? 'item-complete' : 'item-content'">{{items.item}}</label>
		<button class="item-cancel" @click="itemCancel"></button>
	</div>
</li>
</template>

<script>
import './button.css'
import './index.css'
export default{
	props:['items'],
	data (){
		return {
			willShow: true,
			isSelected: false
		}
	},

	methods:{
		itemCancel() {
			this.willShow = false
			this.$emit('itemCancel')
		},
		itemComplete() {
			let toggle = document.getElementsByTagName('input').checked 
			if(this.isSelected == true){
				toggle = false
				this.isSelected = false
			} 
			else {
				toggle = true
				this.isSelected = true 
			}
			this.$emit('itemcomplete',this.isSelected,this.items)
			console.log(this.items.id)
		}
	},
	mounted() {
		
	}
}
</script>

<style>
.content {
	width: 625px;
	height: 55px;
	position: relative;
	top: -59px;
	background-color: #fff;
}
.item-checkbox{
	position: relative;
	left: 20px;
	top: -20px;
}
.item-content{
	font-size: 26px;
	font-weight: lighter;
	position: relative;
	top: -14px;
}
.item-complete{
	font-size: 26px;
	font-weight: lighter;
	position: relative;
	top: -14px;
	opacity: 0.5;
	text-decoration: line-through;

}
.item-cancel {
	border: 0;
    padding: 0;
    background: none;
    font-size: 32px;
    font-weight: lighter;
    position: absolute;
    left: 570px;
    top:  10px;
    opacity: 0.4;
}
.item-cancel:after{
	content: "×";
}
.item-cancel:hover{
	opacity: 0.7;
}
</style>