<template>
    <view>
        <!--标题和返回-->
		<cu-custom :bgColor="NavBarColor" isBack :backRouterName="backRouteName">
			<block slot="backText">返回</block>
			<block slot="content">治具出库</block>
		</cu-custom>
		 <!--表单区域-->
		<view>
			<form>
				<view class="cu-form-group">
				  <view class="flex align-center" style="width: 100%;">
					  <image src="../../static/home/search.png" style="width: 35rpx;height: 35rpx;"/>
				    <input  placeholder="扫描标签二维码" v-model="model.qrcode" @confirm="queryQRcode" style="margin-left: 20rpx;" id="input"/>
					<image src="../../static/home/scan.png" style="width: 50rpx;height: 50rpx;"/>
				  </view>
				</view>
				
				
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">治具编码：</text></view>
                  <input v-model="model.inventoryCode" disabled/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">治具名称：</text></view>
                  <input v-model="model.inventoryName" disabled/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">规格名称：</text></view>
                  <input v-model="model.guigemingcheng" disabled/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center" @click="showtable">
                  <view class="title"><text space="ensp">货位编码：</text></view>
                  <input  placeholder="扫描货位" v-model="model.locationCode"/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">出库数量：</text></view>
                  <input type="number" placeholder="请输入入库数量" v-model="model.num"/>
                </view>
              </view>
			  <view class="cu-form-group">
			    <view class="flex align-center">
			      <view class="title"><text space="ensp">领用人：</text></view>
			      <input placeholder="请扫描领用人" v-model="model.operator"/>
			    </view>
			  </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">当前库存数：</text></view>
                  <input type="number" v-model="model.inventoryQuantity" disabled/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">当前仓库：</text></view>
                  <input v-model="model.warehouse" disabled/>
                </view>
              </view>
              <!-- <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">出库数量：</text></view>
                  <input type="number" placeholder="请输入出库数量" v-model="model.chukuNum"/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">领用人：</text></view>
                  <input  placeholder="请输入领用人" v-model="model.lingyongren"/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">备件编码：</text></view>
                  <input  placeholder="请输入备件编码" v-model="model.beijianbianma"/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">模具名称：</text></view>
                  <input  placeholder="请输入模具名称" v-model="model.mojumingcheng"/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">备件规格：</text></view>
                  <input  placeholder="请输入备件规格" v-model="model.beijianguighe"/>
                </view>
              </view>
              <view class="cu-form-group">
                <view class="flex align-center">
                  <view class="title"><text space="ensp">数量：</text></view>
                  <input type="number" placeholder="请输入数量" v-model="model.num"/>
                </view>
              </view> -->
				<view class="padding">
					<button class="cu-btn block bg-blue margin-tb-sm lg" @click="onSubmit">
						<text v-if="loading" class="cuIcon-loading2 cuIconfont-spin"></text>提交
					</button>
				</view>
			</form>
		</view>
		<view class="cu-modal" :class="{'show': showModal}">
		  <view class="cu-dialog">
		    <view class="table">
		      <view class="tr bg-white">
		        <view class="th">货位编码</view>
		        <view class="th">当前库存数</view>
		      </view>
		      <view class="tr" v-for="(item,index) in record" :key="index" @click="selectLocation(item)">
		        <view class="td">{{ item.locationCode}}</view>
		        <view class="td">{{ item.inventoryQuantity}}</view>
		      </view>
		      <!-- 更多行 -->
		    </view>
		  </view>
		</view>
    </view>
</template>

<script>
    import myDate from '@/components/my-componets/my-date.vue'
Date.prototype.format = function (format) {
           var args = {
               "M+": this.getMonth() + 1,
               "d+": this.getDate(),
               "h+": this.getHours(),
               "m+": this.getMinutes(),
               "s+": this.getSeconds(),
               "q+": Math.floor((this.getMonth() + 3) / 3),  //quarter
               "S": this.getMilliseconds()
           };
           if (/(y+)/.test(format))
               format = format.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
           for (var i in args) {
               var n = args[i];
               if (new RegExp("(" + i + ")").test(format))
                   format = format.replace(RegExp.$1, RegExp.$1.length == 1 ? n : ("00" + n).substr(("" + n).length));
           }
           return format;
       };
    export default {
        name: "BeijianchurukuForm",
        components:{ myDate },
        props:{
          formData:{
              type:Object,
              default:()=>{},
              required:false
          }
        },
        data(){
            return {
				CustomBar: this.CustomBar,
				NavBarColor: this.NavBarColor,
				loading:false,
                model: {},
                backRouteName:'index',
                url: {
                  queryById: "/degson/inventory/queryById",
                  add: "/degson/transactionFlow/add",
                  edit: "/degson/transactionFlow/edit",
				  editInvenstory: "/degson/inventory/edit",
				  query: "/degson/inventory/list",
				  queryMatarial: "/degson/materialZhiju/listByInventoryCode",
				  queryInvenstory:"/degson/inventory/list",
                },
				showModal: false, // 控制模态框的显示状态
				record:[], //存库地点列表
				safeInventory: null,//安全库存数
				num:null,//出库数量
            }
        },
        created(){
             // this.initFormData();
        },
        methods:{
           initFormData(){
               if(this.formData){
                    let dataId = this.formData.dataId;
                    this.$http.get(this.url.queryById,{params:{id:dataId}}).then((res)=>{
                        if(res.data.success){
                            console.log("表单数据",res);
                            this.model = res.data.result;
                        }
                    })
                }
            },
            onSubmit() {
				if(this.model.inventoryCode == "" || this.model.inventoryCode == null || this.model.inventoryCode == undefined){
					uni.showModal({
						title:"警告",
						content:"治具编码不能为空",
						success: (ress) => {
							// if(ress.confirm){
							// 	// 重新加载当前页面，从服务器获取
							// 	// location.reload(true);
							// }
							// // 重新加载当前页面，从服务器获取
							// location.reload(true);
						}
					})
					return false;
				}
				if(this.model.locationCode == "" || this.model.locationCode == null || this.model.locationCode == undefined){
					uni.showModal({
						title:"警告",
						content:"货位编码不能为空",
						success: (ress) => {
							// if(ress.confirm){
							// 	// 重新加载当前页面，从服务器获取
							// 	// location.reload(true);
							// }
							// // 重新加载当前页面，从服务器获取
							// location.reload(true);
						}
					})
					return false;
				}
				if(this.model.num == "" || this.model.num == null || this.model.num == undefined || this.model.num * 1 ==0){
					uni.showModal({
						title:"警告",
						content:"请填写出库数量",
						success: (ress) => {
							// if(ress.confirm){
							// 	// 重新加载当前页面，从服务器获取
							// 	// location.reload(true);
							// }
							// // 重新加载当前页面，从服务器获取
							// location.reload(true);
						}
					})
					return false;
				}
				if(this.model.operator == "" || this.model.operator == null || this.model.operator == undefined){
					uni.showModal({
						title:"警告",
						content:"领用人不能为空",
						success: (ress) => {
							// if(ress.confirm){
							// 	// 重新加载当前页面，从服务器获取
							// 	// location.reload(true);
							// }
							// // 重新加载当前页面，从服务器获取
							// location.reload(true);
						}
					})
					return false;
				}
				this.model.inventoryQuantity -= this.model.num * 1
				this.model.inoutType = 2;
                let myForm = {...this.model};
                this.loading = true;
                let url = this.url.add;
				this.$http.get(this.url.queryMatarial,{params:{inventoryCode:this.model.inventoryCode}}).then(resp=>{
					let form = JSON.parse(JSON.stringify(myForm))
					form.id = null;
					form.transactionDate = new Date().format("yyyy-MM-dd hh:mm:ss")
					form.transactioner = JSON.parse(localStorage.getItem("login_user_info")).data.username
					this.$http.get(this.url.queryInvenstory,{params:{inventoryCode:this.model.inventoryCode,locationCode:this.model.locationCode}}).then(re=>{
					if(this.model.inventoryQuantity * 1 < 0){
																uni.showToast({
																	icon: 'error',
																	title: "注意：现有库存不够，请先入库"+(this.model.inventoryQuantity * -1)+"个",
																	duration: 5000,
																	position: 'bottom',
																})
																this.loading = false;
																this.model.inventoryQuantity += this.model.num * 1
																return false;
					}
					if(this.model.inventoryQuantity * 1 < resp.data.result[0].safeInventory * 1){
												uni.showToast({
													icon: 'error',
													title: "注意：现有库存低于安全库存"+(resp.data.result[0].safeInventory * 1 - this.model.inventoryQuantity * 1)+"个",
													duration: 5000,
													position: 'bottom',
												})
					}
					this.$http.post(url,form).then(res=>{
					   console.log("res",re)
					   // this.loading = false
					   
					   
				if(re.data.success){
					if(re.data.result.records.length > 0){
					var FormRequest = re.data.result.records[0];
					FormRequest.inventoryQuantity = re.data.result.records[0].inventoryQuantity * 1 - this.model.num *1;
					   //更新库存表
					   url = this.url.editInvenstory;
					   this.$http.post(url,FormRequest).then(response=>{
						  console.log("res",response)
						  this.loading = false
						  // this.model = res.data.result.records[0]
						  // this.model.num = num;
						  // this.$Router.push({name:this.backRouteName})
						  uni.showToast({
							icon: 'success',
							title: "提交成功",
							duration: 5000,
							position: 'bottom',
						  })
					   }).catch(()=>{
						this.loading = false
						this.model.inventoryQuantity += this.model.num * 1
						uni.showToast({
							icon: 'error',
							title: "提交失败",
							duration: 5000,
							position: 'bottom',
						})
					   });
					}else{
						uni.showToast({
							icon: 'error',
							title: "提交失败，查不到此货位",
							duration: 5000,
							position: 'bottom',
						})
					}
				}else{
					uni.showToast({
						icon: 'error',
						title: "提交失败",
						duration: 5000,
						position: 'bottom',
					})
				}  // this.$Router.push({name:this.backRouteName})
				this.loading = false
					}).catch(()=>{
						this.loading = false
					});
					}).catch(()=>{
							this.loading = false
							
					});
				});
            },
			queryQRcode(e){
				// uni.showToast({
				// 	title:e.key,
				// 	duration:5000,
				// 	icon:'none',
				// })
				// if(e.key === 'Enter' || e.keyCode === 13){
					this.$nextTick(re=>{
				// console.log(this.model.qrcode.split(',')[0])
				this.model.inventoryCode = e.target.value.split(',')[0]
				this.num = e.target.value.split(',')[1]
				let myForm = {...this.model};
				let url = this.url.query;
				this.$http.get(this.url.queryMatarial,{params:{inventoryCode:this.model.inventoryCode}}).then(resp=>{
					this.safeInventory = resp.data.result[0].safeInventory;
					this.$http.get(url,{params:{inventoryCode:this.model.inventoryCode}}).then(res=>{
					   console.log("res",res)
					   this.loading = false
						   if(res.data.result.records.length > 1){
							   uni.showToast({
								icon: 'error',
								title: "查找到"+res.data.result.records.length+"个库位",
								duration: 5000,
								position: 'bottom',
							   })
							   this.showModal = true;
							   this.record = res.data.result.records;
							   // this.model = res.data.result.records[0];
							   this.model.num = this.num;
						   // return false;
						   }else if(res.data.result.records==0){
								uni.showToast({
									icon: 'error',
									title: "未找到库存",
									duration: 5000,
									position: 'bottom',
								})   
								this.model.qrcode="";
								this.model.num = this.num;
						   }else{
							   this.model = res.data.result.records[0]
							   this.model.num = this.num;
						   }
					   			   
					   // this.$Router.push({name:this.backRouteName})
					}).catch(()=>{
						this.loading = false
						// uni.showToast({
						// 	icon: 'error',
						// 	title: "查询失败",
						// 	duration: 5000,
						// 	position: 'bottom',
						// })
						// // 重新加载当前页面，从服务器获取
						// location.reload(true);
						uni.showModal({
							title:"警告",
							content:"查询失败",
							success: (ress) => {
								if(ress.confirm){
									// 重新加载当前页面，从服务器获取
									// location.reload(true);
								}
								// 重新加载当前页面，从服务器获取
								location.reload(true);
							}
						})
					});
				}).catch(()=>{
						this.loading = false
						// uni.showToast({
						// 	icon: 'error',
						// 	title: "查询失败",
						// 	duration: 5000,
						// 	position: 'bottom',
						// })
						// // 重新加载当前页面，从服务器获取
						// location.reload(true);S
						uni.showModal({
							title:"警告",
							content:"查询失败，"+this.model.inventoryCode+"治具编码没有维护",
							success: (ress) => {
								if(ress.confirm){
									// 重新加载当前页面，从服务器获取
									// location.reload(true);
								}
								// 重新加载当前页面，从服务器获取
								location.reload(true);
							}
						})
					});;
				});
				// }
			},
			selectLocation(item){
				this.model.locationCode = item.locationCode;
				this.model.inventoryQuantity = item.inventoryQuantity;
				this.model.warehouse = item.warehouse;
				this.model.inventoryName = item.inventoryName;
				if(this.model.inventoryQuantity * 1 < this.model.num * 1){
											uni.showToast({
												icon: 'error',
												title: "注意：现有库存不够，请先入库"+(this.model.num * 1 - this.model.inventoryQuantity * 1)+"个",
												duration: 5000,
												position: 'bottom',
											})
											this.showModal = false;
											this.model.qrcode = "";
											return false;
				}
				if(this.model.inventoryQuantity * 1 - this.model.num * 1 < this.safeInventory * 1){
											uni.showToast({
												icon: 'error',
												title: "注意：现有库存低于安全库存"+(this.safeInventory * 1 + this.model.num * 1 - this.model.inventoryQuantity * 1)+"个",
												duration: 5000,
												position: 'bottom',
											})
				}		
				this.showModal = false;
				this.model.qrcode = "";
			},
			showtable(){
				if(this.record.length>1){
					this.showModal = true;
				}
			},
        }
    }
</script>
<style>
	.table { display: table; width: 100%; }
	.tr { display: table-row; }
	.th, .td { display: table-cell; padding: 8px; border: 1px solid #ccc; }
	.th { font-weight: bold; background-color: #f9f9f9; }
</style>
