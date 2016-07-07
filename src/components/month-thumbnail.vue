<template>
	<div class="month-thumbnail" id="{{ thumbId }}" @click="clickThumb">
		<div class="inner-box">
			<header>{{ monthName | uppercase }}</header>
			{{{ dates }}}
		</div>
	</div>
</template>

<script>

import moment from 'moment'

let thumbnailId = ''

export default {

	props: {
		month: {
			type: Number
		},
		year: {
			type: Number
		}
	},
	computed: {
		monthName() {
			return moment([this.year, this.month]).format('MMM')
		},
		dates() {
			let now = moment([this.year, this.month]),
				myMonth = now.format('M'),
				startOfMonth = now.startOf('month').day() - 1,
				daysInMonth = now.daysInMonth(),
				tr = [],
				dcnt = 0

			for (let w = 0; w < 6; w++) {
				let td = []

				for (let d = 0; d < 7; d++) {
					let x = w * 7 + d
 
					if (x > startOfMonth) {
						dcnt++
						if (dcnt <= daysInMonth) {
							td.push('<td>' + dcnt + '</td>')
						}
					} 
					else {
						td.push('<td> </td>')
					}
				}
				tr.push('<tr>' + td.join('\n') + '</tr>')
			}

			return '<table><tbody>' + tr.join('\n') + '</tbody></table>'
		},
		thumbId() {
			this.thumbnailId = 'thumb-' + moment([this.year, this.month]).format('YYYYMM')
			return this.thumbnailId
		}
	},
	events: {},
	methods: {
		clickThumb() {
			this.$dispatch( 'month-thumbnail-select', this )
		}
	},
	components: {
		// component
	}
}

</script>

<style lang="scss">
.month-thumbnail {
	display: inline-block;
	width: 32.5%;
	pointer-events: normal;
	cursor: pointer;
	.inner-box {
		margin: 4px;
		header {
			font-size: 12px;
			font-weight: bold;
			text-align: center;
		}
		table {
			width: 99.5%;
			border-collapse: separate;
			border-spacing: 2px;
			td {
				font-size: 9px;
				text-align: right;
			}
		}
	}
}
</style>