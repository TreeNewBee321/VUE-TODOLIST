<template>
	<div class="todo-wrapper">
		<h1>TODOS</h1>
		<div>
			<input type="text" class = "todo-new" placeholder = "What need to be done?" v-model = "item">
			<button class = "add-new-todo" @click = "submit">ADD</button>
			<input class = "toggle" type = "checkbox">
			<label class = "toggle"></label>
		</div>
		<ul class="item-list" v-if="willShow === 1" ref="disItem">
		    <display-item  v-for = "item in itemList" :items = "item" v-on:itemcomplete = "setAttribute" >	
			</display-item>
		</ul>
		<ul class="item-list" v-else-if="willShow === 2" ref="disItem">
		    <display-item  v-for = "item in activeList" :items = "item" v-on:itemcomplete = "setAttribute" >	
			</display-item>
		</ul>
		<ul class="item-list" v-else="willShow === 3" ref="disItem">
		    <display-item  v-for = "item in completeList" :items = "item" v-on:itemcomplete = "setAttribute" >	
			</display-item>
		</ul>
		<div class="footer">
			<label class="item-left">{{activeList.length }}item is going to do</label>
			<button class="all" @click="allItem" >All</button>
			<button class="active" @click="activeItem">Active</button>
			<button class="complete" @click="completeItem">Complete</button>
			<button class="clear" @click="hideDiv" >clear</button>
		</div>		
	</div>
</template>

<script>
import DisplayItem from './DisplayItem'
export default{
	components: {
		DisplayItem
	},

	data() {
		return {
			willShow: 1,
			itemNumbers: 0,
			itemList: [],
			completeList: [],
			activeList: [],
			activeList: [],
			item: '',
			id: -1,
			index1: -1,
			index2: -1,

		}
	},

	methods: {
        submit() {
			this.willShow = 1;
			if(this.item !== '') {
				this.id = this.id + 1;
				this.itemNumbers = this.itemNumbers+1
				const message = {
					item: this.item,
					id: this.id,
					index1:this.index1,
					index2:this.id,
				}
				this.itemList.push(message);
				this.activeList.push(message);
			}
		},

		/*itemReduce() {
			this.itemNumbers = this.itemNumbers - 1
			console.log(this.itemNumbers)
		},*/
		setAttribute(isSelected,items) {			
			//this.$refs.disItem.childNodes[items.id].getElementsByTagName("input").checked = isSelected
			//console.log(this.$refs.disItem.childNodes[0].getElementsByTagName("input").checked)
			//this.itemList.splice(items.id,1)
			if(isSelected) {
				this.completeList.push(items)
				this.activeList.splice(items.index2,1)
				items.index1 = this.completeList.length - 1
			} else {
				this.completeList.splice(items.index1,1)
				this.activeList.push(items)
				items.index2 = this.activeList.length - 1
			}
			console.log("item"+this.itemList.length)
			console.log("complete"+this.completeList.length)
		},
		hideDiv() {
			this.completeList = []					 
		},
		allItem() {
			this.willShow = 1
		},
		activeItem() {
			//let total = document.querySelector(".item-list").childNodes.length
			//console.log(this.$refs.disItem.childNodes[0].getElementsByTagName("input").checked)
			this.willShow = 2			
		},
		completeItem() {
			this.willShow = 3
		}

	},
	mounted() {
	}
}
</script>

<style>
body {
	background-color: #f5f5f5;
}
h1 {
	font-size: 100px;
	color: #70dcb5;
	font-family: "NanumGothic";
	text-align: center;
	font-weight: lighter;
	opacity: 0.7;
}
.todo-wrapper {
	width: 625px;
	margin: 0 auto;
}

.todo-new {
	position: relative;
	margin: 0;
	width: 550px;
	font-size: 24px;
	font-family: inherit;
	font-weight: lighter;
	line-height: 1.4em;
	border: 0;
	outline: none;
	color: #000;
	padding: 6px;
	border: 1px solid #999;
	padding: 16px 16px 16px 60px;
	border: none;
	/*box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2)*/
}
.add-new-todo {
	height: 61px;
	width: 100px;
	outline: none;
	border: none;
	position: relative;
	left: 525px;
	top: -63.6px;
	font-size: 24px;
	font-weight: bold;
	color: white;
	background-color: #e5e5e5
}

.add-new-todo:hover {
	background-color: #d5d5d5;
}

.toggle {
	position: relative;
	top: -65px;
	left: -110px;
	width: 60px;
	height: 34px;
	text-align: center;
	border: none; 
	background: none;
	transform: rotate(180deg);
}
.toggle:before{
	content: '❯';
	font-size: 22px;
	color: #999;
	padding: 10px 27px 10px 27px;
}
input[type='checkbox'] {
  display: none;
}
input[type='checkbox']:checked+label {
  background-position: 0 -60px;
}

.item-list{
	margin: 0;
	padding: 0;
}
.footer {
	border-left: none;
	border-right: none;
	width: 100%;
	height: 50px;
	background-color: #fff;
	padding: 0;
	position: relative;
	top: -59px;
	line-height: 50px;
}
.all, .active, .complete, .clear{
	background: none;
	font-size: 14px;
	position: relative;
	border-radius: 10px;
	top: -0px !important;
}
.all{
	left: -120px;
	top:20px;
}
.active {
	left: -80px;
	top: 20px;
}
.complete {
	left: -40px;
	top: 20px;
}
.clear {
	left: 100px;
	top: 20px;
}
.item-left{
	position: relative;
	left: -170px;
	top: -0px;
}
</style>