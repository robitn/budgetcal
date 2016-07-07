<template>
	<div class="year-view">
		<month-thumbnail v-for="month in 12" :month="month" :year="currentYear"></month-thumbnail>
	</div>
</template>

<script>
import MonthThumbnail from './month-thumbnail'

export default {

	props: {
		currentYear: {
			type: Number,
			required: true
		}
	},
	computed: {
		breakRow: function () {
			if (this.month % 3 == 0) {
				return '<br>'
			}
			return '\n'
		}
	},
	events: {
		'month-thumbnail-select': function (data) {
			console.log( data );
			alert('Expand thumbnail: "' + data.thumbId + '"\n' 
				+ "top:    " + data.$el.offsetTop + ',\n' 
				+ "left:    " + data.$el.offsetLeft + ', \n'
				+ "width:  " + data.$el.offsetWidth + ', \n'
				+ "height: " + data.$el.offsetHeight )
		}
	},
	methods: {},
	data () {
		return {}
	},
	components: {
		MonthThumbnail
	},
	ready: function () {
		// console.log( this );
	}
}

</script>

<style lang="scss">

.year-view {
	max-width: 360px;
	margin-right: auto;
	margin-left: auto;
}

</style>