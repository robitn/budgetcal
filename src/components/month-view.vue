<template>
	<div class="month-view" transition="slide" v-show="show">
		<span class="back" @click.stop="hideMe">&nbsp;<i class="fa fa-angle-left fa-2x"><span>{{ shortMonthName }} {{ year }}</span></i></span>
		<br><br>
		&nbsp;{{ year }}, {{ today }}
		
	</div>
</template>

<script>

import moment from 'moment'

let show = false,
	year = 0,
	month = 0,
	today = 0,
	monthName = '',
	shortMonthName = ''

export default {

	data() {
		return { show, year, month, today, monthName, shortMonthName }
	},
	computed: {
	},
	events: {
		'show-month-view': function(data) {
			console.log( data );
			this.month = data.month
			this.today = data.today
			this.year = data.year
			this.monthName = moment([this.year, this.month]).format('MMMM')
			this.shortMonthName = data.monthName
			this.show = true
		},
		'hide-month-view': function() {
			this.show = false
		}
	},
	methods: {
		hideMe() {
			this.$dispatch('hide-month-view')
			this.show = false
		}
	},
	components: {},
	transitions: {
		beforeLeave() {
			console.log('month-view : afterLeave');
		},
		beforeEnter: function(el) {
			console.log('month-view : afterEnter');
		}
	}
}

</script>

<style lang="scss">

.month-view {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-color: white;
	span.back {
		font-size: 16px;
		color: red;
		cursor: pointer;
		i > span {
			display: inline-block;
			font-size: 16px;
			font-family: "Helvetica Neue", Helvetica, sans-serif;
			vertical-align: middle;
			padding: 2px 0 4px 8px;
		}
	}
	&.slide-transition {
		transition: transform 0.4s ease, box-shadow 0.4s ease;
		transform: translate3d(0%, 0, 0);
		box-shadow: -35px 0 150px lightgrey;
		&.slide-enter, &.slide-leave {
			transform: translate3d(100%, 0, 0);
			box-shadow: -1px 0 3px lightgrey;
		}
	}
}
</style>