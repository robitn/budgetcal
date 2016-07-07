<template>
	<div id="app">
		<year-view :current-year="year"></year-view>
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

	computed: {
		year: function () {
			return moment().year() 
		}
	},
	components: {
		YearView,
		MonthView,
		AddEditForm
	}
}
</script>

<style>
body {
	font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
	font-weight: 200;
}
</style>
