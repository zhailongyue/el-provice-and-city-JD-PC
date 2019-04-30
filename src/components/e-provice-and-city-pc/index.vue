<template>
	<div class="provideAndCity">
		<div style="display: inline-block">
			<div class="distributionBox" @mouseleave="isDiosShow = false">
				<!-- 显示内容 -->
				<div class="distributionLabel" :style="{width:labelWidthHtml}" @mouseover="isDiosShow = true">
					<div v-html="address" :style="{width:labelAddressHtml}"></div>
					<i class="el-icon-arrow-down"></i>
				</div>
				<div class="distributionDio" :style="{width:distributionDioHtml}" v-show="isDiosShow">
					<el-tabs v-model="activeName" type="border-card">
						<el-tab-pane :label="labelFirst" name="first">
							<el-tag v-for="(item,index) in proviceList" :key="index" v-bind="{type:index === numFirst ? 'warning' : 'info'}"
							 @click="tagsClickFirst(index, item)">{{item.name}}</el-tag>
						</el-tab-pane>
						<el-tab-pane :label="labelSecond" name="second" v-if='cityList.length > 0'>
							<el-tag v-for="(item,index) in cityList" :key="index" v-bind="{type:index === numSecond ? 'warning' : 'info'}"
							 @click="tagsClickSecond(index, item)">{{item.name}}</el-tag>
						</el-tab-pane>
						<el-tab-pane :label="labelThird" name="third" v-if='areaList.length > 0'>
							<el-tag v-for="(item,index) in areaList" :key="index" v-bind="{type:index === numThird ? 'warning' : 'info'}"
							 @click="tagsClickThird(index, item)">{{item.name}}</el-tag>
						</el-tab-pane>
						<el-tab-pane :label="labelFourth" name="fourth" v-if='streetList.length > 0'>
							<el-tag v-for="(item,index) in streetList" :key="index" v-bind="{type:index === numFourth ? 'warning' : 'info'}"
							 @click="tagsClickFourth(index, item)">{{item.name}}</el-tag>
						</el-tab-pane>
					</el-tabs>
					<div class="line" :style="{width:lineHtml}"></div>
					<!-- X -->
					<i class="el-icon-close" @click="isDiosShow = false"></i>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: "provideAndCity",
		props: {
			labelWidth: {//自定义宽度 建议不要小于250
				type: Number,
				default: () => 300
			},
			provideAndCityBox: {
				type: Object,
				default: () => {
					return { //赋值值时使用
						address: "", //地址
						labelFirst: "", //省label
						labelSecond: "", //市label
						labelThird: "", //区label
						labelFourth: "", //街道label
						proviceList: [], //省列表
						cityList: [], //市列表
						areaList: [], //区列表
						streetList: [], //街道列表
						proviceCode: '',
						cityCode: '',
						areaCode: '',
						streetCode: '',
					}
				}
			}
		},
		data() {
			return {
				labelWidthHtml: '',
				distributionDioHtml: '',
				lineHtml: '',
				labelAddressHtml: '',
				activeName: "first",
				numFirst: "",
				numSecond: "",
				numThird: "",
				numFourth: "",
				isDiosShow: false,
				address: "",
				labelFirst: "请选择",
				labelSecond: "请选择",
				labelThird: "请选择",
				labelFourth: "请选择",
				proviceList: [],
				cityList: [],
				areaList: [],
				streetList: [],
				proviceCode: '',
				cityCode: '',
				areaCode: '',
				streetCode: '',
			};
		},
		created() {
			// 文本框宽度
			this.labelWidthHtml = this.labelWidth + 'px'
			this.distributionDioHtml = this.labelWidth + this.labelWidth * 2 / 3 + 'px'
			this.lineHtml = this.labelWidth * 2 / 3 + 'px'
			this.labelAddressHtml = this.labelWidth - 30 + 'px'
			this.getAddressList("", "provice");
		},
		mounted() {
			if (this.provideAndCityBox.address) {
				this.address = this.provideAndCityBox.address || ''
				this.labelFirst = this.provideAndCityBox.labelFirst || '请选择'
				this.labelSecond = this.provideAndCityBox.labelSecond || '请选择'
				this.labelThird = this.provideAndCityBox.labelThird || '请选择'
				this.labelFourth = this.provideAndCityBox.labelFourth || '请选择'
				this.proviceList = this.provideAndCityBox.proviceList || []
				this.cityList = this.provideAndCityBox.cityList || []
				this.areaList = this.provideAndCityBox.areaList || []
				this.streetList = this.provideAndCityBox.streetList || []
				this.proviceCode = this.provideAndCityBox.proviceCode || ''
				this.cityCode = this.provideAndCityBox.cityCode || ''
				this.areaCode = this.provideAndCityBox.areaCode || ''
				this.streetCode = this.provideAndCityBox.streetCode || ''
			}
		},
		methods: {
			// 获取地址
			getAddressList(id, type) {
				if (type === "provice" || type === '') {
					//this.proviceList = res; //接口请求后赋值
					this.proviceList = [{
							name: "山西",
							code: "1"
						},
						{
							name: "山东",
							code: "2"
						},
						{
							name: "浙江",
							code: "3"
						},
						{
							name: "黑龙江",
							code: "4"
						},
						{
							name: "河北",
							code: "5"
						},
						{
							name: "吉林",
							code: "6"
						},
						{
							name: "测试省",
							code: "7"
						}
					]
					return false;
					this.cityList = [];
					this.areaList = [];
					this.streetList = [];

					this.numSecond = "";
					this.numThird = "";
					this.numFourth = "";

					this.labelSecond = "请选择";
					this.labelThird = "请选择";
					this.labelFourth = "请选择";
				} else if (type === "city") {
					// this.cityList = res; //接口请求后赋值
					this.cityList = [{
							name: "北北京北京北京北京北京京",
							code: "1"
						},
						{
							name: "上海",
							code: "2"
						},
						{
							name: "杭州",
							code: "3"
						},
						{
							name: "广州",
							code: "4"
						},
						{
							name: "哈尔滨",
							code: "5"
						},
						{
							name: "合肥",
							code: "6"
						},
						{
							name: "测试市",
							code: "7"
						}
					];

					this.areaList = [];
					this.streetList = [];

					this.numSecond = "";
					this.numThird = "";
					this.numFourth = "";

					this.labelSecond = "请选择";
					this.labelThird = "请选择";
					this.labelFourth = "请选择";


					if (this.cityList.length > 0) {
						this.activeName = "second";
					}
				} else if (type === "area") {
					// this.areaList = res; //接口请求后赋值
					this.areaList = [{
							name: "天桥区",
							code: "1"
						},
						{
							name: "上城区",
							code: "2"
						},
						{
							name: "背囊区背囊区背囊区",
							code: "3"
						},
						{
							name: "啥啊区",
							code: "4"
						},
						{
							name: "就好区",
							code: "5"
						},
						{
							name: "个键区",
							code: "6"
						},
						{
							name: "测试区",
							code: "7"
						}
					];
					this.streetList = [];

					this.numThird = "";
					this.numFourth = "";

					this.labelThird = "请选择";
					this.labelFourth = "请选择";


					if (this.areaList.length > 0) {
						this.activeName = "third";
					} else {
						this.isDiosShow = false;
					}
				} else if (type === "street") {
					// this.streetList = res; //接口请求后赋值
					this.streetList = [{
							name: "天桥街道",
							code: "1"
						},
						{
							name: "上城街道",
							code: "2"
						},
						{
							name: "背囊街道",
							code: "3"
						},
						{
							name: "啥啊街道",
							code: "4"
						},
						{
							name: "就好街道",
							code: "5"
						},
						{
							name: "个键街道",
							code: "6"
						},
						{
							name: "测试街道",
							code: "7"
						}
					];
					this.numFourth = "";

					this.labelFourth = "请选择";
					if (this.streetList.length > 0) {
						this.activeName = "fourth";
					} else {
						this.isDiosShow = false;
					}
				}
			},
			// tags点击 省
			tagsClickFirst(type, param) {
				this.numFirst = type;
				this.address = param.name;
				this.labelFirst = param.name;
				this.proviceCode = param.code;
				// this.getAddressList(param.code, "city");
				this.paramEmit(param.code, "city");
			},
			// tags点击 市
			tagsClickSecond(type, param) {
				this.numSecond = type;
				this.address = this.labelFirst + "/" + param.name;
				this.cityCode = param.code;
				this.labelSecond = param.name;
				// this.getAddressList(param.code, "area");
				this.paramEmit(param.code, "area");
			},
			// tags点击 区
			tagsClickThird(type, param) {
				this.numThird = type;
				this.address =
					this.labelFirst + "/" + this.labelSecond + "/" + param.name;
				this.labelThird = param.name;
				this.areaCode = param.code;
				// this.getAddressList(param.code, "street");
				this.paramEmit(param.code, "street");
			},
			// tags点击 街道
			tagsClickFourth(type, param) {
				this.numFourth = type;
				this.address =
					this.labelFirst +
					"/" +
					this.labelSecond +
					"/" +
					this.labelThird +
					"/" +
					param.name;
				this.streetCode = param.code;
				this.labelFourth = param.name;
				this.paramEmit(param.code, '');
			},
			//输出
			paramEmit(id, type) {
				let param = {
					address: this.address, //拼接后的地址
					proviceCode: this.proviceCode, //省code
					cityCode: this.proviceCode, //市code
					areaCode: this.proviceCode, //区code
					streetCode: this.proviceCode, //街道code
					proviceName: this.labelFirst, //省code
					cityName: this.labelSecond, //市code
					areaName: this.labelThird, //区code
					streetName: this.labelFourth, //街道code
					typeAdnId: {
						id: id,
						type: type
					}
				}
				this.$emit('proviceAndCity', param)
			}
		}
	};
</script>
<style lang="scss">
	// 大盒子
	.distributionBox {
		position: relative;
		display: inline-block;

		// width: 250px;
		// float: left;
		// 文本框
		.distributionLabel {
			// width: 250px;
			height: 30px;
			line-height: 30px;
			border: solid 1px #cccccc;
			border-radius: 3px;
			position: relative;

			i {
				position: absolute;
				right: 10px;
				top: 9px;
			}

			div {
				text-align: left;
				font-size: 12px;
				padding: 0 10px;
				width: 100%;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
			}
		}

		.distributionDio {
			z-index: 1;
			width: 420px;
			min-height: 200px;
			background: #fff;
			border: solid 1px #ccc;
			border-top: 0;
			border-radius: 0 0 2px 2px;
			position: absolute;
			left: 0;
			top: 28px;
			padding: 5px 0 0 0;

			.el-tabs--border-card {
				border: none;
				box-shadow: none;
				-webkit-box-shadow: none;
			}

			.el-tabs--border-card>.el-tabs__header {
				background: #fff;

				.el-tabs__nav-scroll {
					line-height: 30px;

					.el-tabs--border-card>.el-tabs__header .el-tabs__item.is-active {
						color: #f26632;
					}

					.el-tabs__item.is-active {
						color: #f26632;
						border-top: solid 1px #cccccc;
					}

					.el-tabs__item:hover {
						color: #f26632;
						border-top: solid 1px #cccccc;
					}

					.el-tabs__item {
						font-size: 12px;
						padding: 0 15px;
						height: 30px;
						line-height: 30px;
					}
				}
			}

			.el-tabs--border-card>.el-tabs__content {
				padding: 5px;
				font-size: 12px;
				text-align: left;

				.el-tag {
					padding: 0 10px;
					height: 22px;
					line-height: 20px;
					cursor: pointer;
					margin: 5px 2px;
				}
			}

			.line {
				position: absolute;
				right: -1px;
				top: -1px;
				width: 170px;
				height: 1px;
				background: #ccc;
			}

			.el-icon-close {
				position: absolute;
				right: 10px;
				top: 10px;
				cursor: pointer;
			}
		}
	}
</style>
