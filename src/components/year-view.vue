<template>
	<div class="year-view" transition="hyde" v-show="show">
		<month-thumbnail v-for="month in 12" :month="month" :year="currentYear" :today="today"></month-thumbnail>
	</div>
</template>

<script>
import MonthThumbnail from './month-thumbnail'

let show = true

export default {

	props: {
		currentYear: {
			type: Number,
			required: true
		},
		today: {
			type: String,
			required: true
		}
	},
	data() {
		return {
			show
		}
	},
	computed: {},
	events: {
		'show-month-view': function(data) {
			this.show = false
		},
		'hide-month-view': function() {
			this.show = true
		}
	},
	methods: {
		hideMe() {
			this.$dispatch('hide-month-view')
			this.show = false
		}
	},
	components: {
		MonthThumbnail
	},
	ready: function () {
		this.$broadcast('remove-badges')
		this.$broadcast('badge-today', '#ds-' + this.today)
	}
}

</script>

<style lang="scss">

.year-view {
	max-width: 360px;
	margin-right: auto;
	margin-left: auto;
	&.hyde-transition {
		transition: transform 0.3s ease;
		transform: translate3d(0, 0, 0);
		&.hyde-enter, &.hyde-leave {
			transform: scale3d(0.9, 1, 1) translate3d(-20%, 0, 0);
		}
	}
}

</style>