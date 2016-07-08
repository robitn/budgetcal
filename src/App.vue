<template>
	<div id="app">
		<year-view :today="today" :current-year="year"></year-view>
		<month-view></month-view>
		<add-edit-form></add-edit-form>
	</div>
</template>

<script>
import YearView from './components/year-view'
import MonthView from './components/month-view'
import AddEditForm from './components/add-edit-form'
import moment from 'moment'

let year = 0

export default {

	data() {
		return {}
	},
	computed: {
		year() {
			return moment().year() 
		},
		today() {
			return moment().format('YYYYMMDD')
		}
	},
	events: {
		'month-thumbnail-select': function (data) {
			this.$broadcast('show-month-view', data)
		},
		'hide-month-view': function () {
			this.$broadcast('hide-month-view')
		}
	},
	components: {
		YearView,
		MonthView,
		AddEditForm
	},
	ready() {
		let that = this
	}
}
</script>

<style>
html, body {
	height: 100%;
}
body {
	position: relative;
	font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
	font-weight: 200;
}
</style>
