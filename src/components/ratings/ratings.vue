<template>
  <cube-scroll ref="scroll" class="rating-wrap" :options="scrollOptions">
	<div class="rating">
		<div class="overview">
			<div class="overview-left">
				<div class="score">{{seller.score}}</div>
				<div class="text">综合评分</div>
				<div class="desc">高于周边商家{{seller.rankRate}}%</div>
			</div>
			<div class="overview-right">
				<div class="star-wrap1">
					<span class="name">服务态度</span>
					<star :size=2 :score="seller.serviceScore" class="star"></star>
					<span class="text">{{seller.serviceScore}}</span>
				</div>
				<div class="star-wrap1">
					<span class="name">商品评分</span>
					<star :size=2 :score="seller.foodScore" class="star"></star>
					<span class="text">{{seller.foodScore}}</span>
				</div>
				<div class="delivery">
					<span class="name">送达时间</span>
					<span class="time">{{seller.deliveryTime}}分钟</span>
				</div>
			</div>
		</div>
		<split></split>
		<rating-select 
			:ratings="ratings" 
			:selectType="selectType"
			:onlyContent="onlyContent"
			@select="onSelect"
			@toggle="onToggle">
		</rating-select>
		<ul class="list">
			<li class="list-item" v-for="item in computedRatings">
				<div class="avatar-wrap"><img :src="item.avatar" width="28px" height="28px"/></div>
				<div class="content">
					<div class="user">{{item.username}}</div>
				</div>
				<div class="star-info">
					<star :size=1 :score="item.score" class="star"></star>
					<div class="delivery" v-show="item.deliveryTime">{{item.deliveryTime}}分钟送达</div>
				</div>
				<div class="text">{{item.text}}</div>
				<div class="recommend" v-show="item.recommend">
					<span class="item" v-for="recommend in item.recommend">{{recommend}}</span>
				</div>
				<div class="time">{{formateTime(item.rateTime)}}</div>
			</li>
		</ul>
	</div>
  </cube-scroll>
</template>

<script>
import moment from 'moment'
import Star from 'components/star/star'
import Split from 'components/split/split'
import RatingSelect from 'components/rating-select/rating-select'
import {getRatings} from 'api'

const ALL=2
export default {
  data(){
    return {
	  ratings: [],
	  scrollOptions: {
		click: false,
		directionLockThreshold: 0
	  },
	  selectType: ALL,
	  onlyContent: false
    }
  },
  props: {
    data: {
	  type: Object,
	  default() {
		  return {}
	  }
    }
  },
  computed: {
    seller() {
	  return this.data.seller
    },
	computedRatings() {
		let ret = []
		this.ratings.forEach((rating) => {
			if (this.onlyContent && !rating.text) {
				return
			}
			if (this.selectType === ALL || rating.rateType === this.selectType) {
				ret.push(rating)
			}
		})
		return ret
	}
  },
  methods:{
	  fetch(){
	  	if(!this.fetched){
	  		this.fetched=true
	  		getRatings().then(ratings=>{
	  			this.ratings=ratings
	  		})
	  	}
	  },
	  onSelect(type) {
		  this.selectType=type
	  },
	  onToggle(){
		console.log(1)
	  	this.onlyContent=!this.onlyContent
	  },
	  formateTime(time){
	  	return moment(time).format('YYYY-MM-DD hh:mm')
	  }
  },
  components: {
	Star,
	Split,
	RatingSelect
  }
}
</script>

<style lang="stylus" scoped>
.rating-wrap
	position: relative
	height: 100%
	width: 100%
	.overview
		display: flex
		padding: 18px 0
		.overview-left
			flex: 0 0 138px
			width: 138px
			text-align: center
			border-right: 1px solid #e6e7e8
			@media only screen and (max-width: 320px)
				flex: 0 0 110px
				width: 110px
			.score
				line-height: 28px
				font-size: 24px
				color: #ff9900
			.text
				line-height: 24px
				font-size: 12px
				color: #07111b
			.desc
				line-height: 14px
				font-size: 10px
				color: #93999f
				padding-bottom: 4px
		.overview-right
			flex: 1
			padding-left: 24px
			@media only screen and (max-width: 320px)
				padding-left: 12px
			.star-wrap1
				display: flex
				align-items: center
				margin-bottom: 8px
				.name
					line-height: 18px
					font-size: 12px
					color: #07111b
				.star
					margin: 0 12px
				.text
					line-height: 18px
					font-size: 12px
					color: #ff9900
			.delivery
				font-size: 0
				.name
					display: inline-block
					line-height: 18px
					font-size: 12px
					color: #07111b
				.time
					margin-left: 12px
					display: inline-block
					line-height: 18px
					font-size: 12px
					color: #93999f
					
</style>
