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
		today: {
			type: String
		},
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
							let timeStamp = now.date(dcnt).format('YYYYMMDD'),
								tdTag = '<td id="ds-' + timeStamp + '">'

							td.push(tdTag + '<span>' + dcnt + '</span>' + '</td>')
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
	events: {
		'badge-today' : function (data) {
			let myEl = document.querySelector(data)

			myEl.className = 'today'
		},
		'remove-badges': function () {
			let myEls = document.querySelectorAll('#' + this.thumbnailId + ' td')

			for (let el in myEls) {
				if (!isNaN(el)) {
					myEls[el].classList.remove('today')
				}
			}			
		}
	},
	methods: {
		clickThumb() {
			this.$dispatch('month-thumbnail-select', this)
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
			padding-bottom: 0;
			font-size: 12px;
			font-weight: bold;
			text-align: center;
		}
		table {
			width: 99.5%;
			border-collapse: separate;
			border-spacing: 2px;
			td {
				line-height: 1;
				span {
					display: inline-block;
					width: 12px;
					height: 12px;
					border-radius: 10px;
					line-height: 1.4;
					font-size: 9px;
					text-align: center;
				}
			}
		}
	}
	td.today {
		span {
			background-color: red;
			color: white;
		}
	}
}
</style>