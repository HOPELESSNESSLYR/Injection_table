<template>
    <view>
        <!--标题和返回-->
		<cu-custom :bgColor="NavBarColor" isBack :backRouteName="backRouteName">
			<block slot="backText">返回</block>
			<block slot="content">注塑成型工艺表</block>
		</cu-custom>
		
		<!-- 表格区域 -->
		<view class="table-container">
			<view class="table-section">
				<view class="table-header">注塑成型工艺表</view>
				<view class="table-row">
					<view class="table-cell">文件编号</view>
					<view class="table-cell"><input placeholder="如QP-003-03" v-model="model.processTableNumber"/></view>
					<view class="table-cell">版本</view>
					<view class="table-cell"><input placeholder="如1.3" v-model="model.version"/></view>
				</view>
				
				<view class="table-row">
					<view class="table-cell">机号</view>
					<view class="table-cell"><input v-model="model.machineNumber"/></view>
					<view class="table-cell">资产编码</view>
					<view class="table-cell"><input v-model="model.assetCode"/></view>
					<view class="table-cell">机型</view>
					<view class="table-cell"><input v-model="model.machineModel"/></view>
				</view>

				<view class="table-row">
					<view class="table-cell">料号</view>
					<view class="table-cell"><input placeholder="材料料号" v-model="model.materialCode"/></view>
					<view class="table-cell">品名</view>
					<view class="table-cell"><input placeholder="产品名称" v-model="model.productName"/></view>
					
				</view>
				<view class="table-row">
					<view class="table-cell">模具编号</view>
					<view class="table-cell"><input v-model="model.moldNumber"/></view>
					<view class="table-cell">模穴数</view>
					<view class="table-cell"><input v-model="model.cavityCount"/></view>
					<view class="table-cell">实取数</view>
					<view class="table-cell"><input type="number" v-model="model.actualCavityCount"/></view>
					
				</view>
				<view class="table-row">
					<view class="table-cell">材质</view>
					<view class="table-cell"><input placeholder="材料类型/材质" v-model="model.materialType"/></view>
					<view class="table-cell">产品单重</view>
					<view class="table-cell"><input type="number" v-model="model.productWeight"/></view>
					<view class="table-cell">水口重量</view>
					<view class="table-cell"><input type="number" v-model="model.runnerWeight"/></view>
				</view>
				
				<view class="table-row">
					<view class="table-cell">螺杆</view>
					<view class="table-cell"><input type="number" v-model="model.screwDiameter"/></view>
					<view class="table-cell">色号</view>
					<view class="table-cell"><input v-model="model.colorCode"/></view>
					<view class="table-cell">日期</view>
					<view class="table-cell">
						<!-- <my-date fields="day" v-model="model.processDate" placeholder="工艺制定日期"></my-date> -->
						<input placeholder="格式:2023.08.07" v-model="model.processDate"/>
					</view>
					<view class="table-cell">周期</view>
					<view class="table-cell"><input type="number" v-model="model.cycleTime"/></view>
				</view>

			</view>

			<!-- 温度控制参数 -->
			<view class="table-section">
				<view class="table-header">炮台温控参数</view>
				<view class="table-row table-header-row">
						<view class="table-cell">主射台</view>
						<view class="table-cell">段数</view>
						<view class="table-cell">T1</view>
						<view class="table-cell">T2</view>
						<view class="table-cell">T3</view>
						<view class="table-cell">T4</view>
						<view class="table-cell">T5</view>
				</view>
				<view class="table-row">
						<view class="table-cell"></view>
						<view class="table-cell">设定</view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT1Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT2Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT3Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT4Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT5Set" /></view>

				</view>
				<view class="table-row">
						<view class="table-cell"></view>
						<view class="table-cell">实际</view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT1Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT2Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT3Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT4Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.mainBarrelT5Actual" /></view>
				</view>
				<view class="table-row table-header-row">
						<view class="table-cell">副射台</view>
						<view class="table-cell">段数</view>
						<view class="table-cell">T1</view>
						<view class="table-cell">T2</view>
						<view class="table-cell">T3</view>
						<view class="table-cell">T4</view>
						<view class="table-cell">T5</view>
				</view>
				<view class="table-row">
						<view class="table-cell"></view>
						<view class="table-cell">设定</view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT1Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT2Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT3Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT4Set" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT5Set" /></view>
				
				</view>
				<view class="table-row">
						<view class="table-cell"></view>
						<view class="table-cell">实际</view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT1Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT2Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT3Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT4Actual" /></view>
						<view class="table-cell"><input type="number" v-model="model.subBarrelT5Actual" /></view>
						
				</view>
				<view class="table-row">
					<view class="table-cell">模温控制</view>
					<view class="table-cell">前模</view>
					<view class="table-cell"><input type="number" v-model="model.frontMoldTempSet" /></view>
					<view class="table-cell">实际</view>
					<view class="table-cell"><input type="number" v-model="model.frontMoldTempActual" /></view>
					<view class="table-cell">后模</view>
					<view class="table-cell"><input type="number" v-model="model.rearMoldTempSet" /></view>
					<view class="table-cell">实际</view>
					<view class="table-cell"><input type="number" v-model="model.rearMoldTempActual" /></view>
				</view>
				
			</view>
	<!-- 			<view class="table-subheader">主射台温控</view> -->
				<!-- <view class="table-row">
					<view class="table-cell">T1 设定/实际</view>
					<view class="table-cell">
					</view>
					<view class="table-cell">T2 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.mainBarrelT2Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.mainBarrelT2Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T3 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.mainBarrelT3Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.mainBarrelT3Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T4 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.mainBarrelT4Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.mainBarrelT4Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T5 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.mainBarrelT5Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.mainBarrelT5Actual" style="width:45%"/>
					</view>
				</view> 

				<view class="table-subheader">副射台温控</view>
				<view class="table-row">
					<view class="table-cell">T1 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.subBarrelT1Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.subBarrelT1Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T2 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.subBarrelT2Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.subBarrelT2Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T3 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.subBarrelT3Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.subBarrelT3Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T4 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.subBarrelT4Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.subBarrelT4Actual" style="width:45%"/>
					</view>
					<view class="table-cell">T5 设定/实际</view>
					<view class="table-cell">
						<input type="number" placeholder="设定" v-model="model.subBarrelT5Set" style="width:45%"/>
						<input type="number" placeholder="实际" v-model="model.subBarrelT5Actual" style="width:45%"/>
					</view>
				</view>-->
				
		 
			
<!-- 			

			<view class="table-subheader">模温控制u</view>
			<view class="table-row">
			    <view class="table-cell">前模温度 设定/实际</view>
			    <view class="table-cell">
			        <input type="number" placeholder="设定" v-model="model.frontMoldTempSet" style="width:45%"/>
			        <input type="number" placeholder="实际" v-model="model.frontMoldTempActual" style="width:45%"/>
			    </view>
			    <view class="table-cell">后模温度 设定/实际</view>
			    <view class="table-cell">
			        <input type="number" placeholder="设定" v-model="model.rearMoldTempSet" style="width:45%"/>
			        <input type="number" placeholder="实际" v-model="model.rearMoldTempActual" style="width:45%"/>
			    </view>
			</view>
			

			<view class="table-subheader">干燥参数</view>
			 -->
			
			<view class="table-header">热流道温控参数</view>
			<view class="table-row table-header-row">
					<view class="table-cell">T1</view>
					<view class="table-cell">T2</view>
					<view class="table-cell">T3</view>
					<view class="table-cell">T4</view>
					<view class="table-cell">T5</view>
					<view class="table-cell">T6</view>
					<view class="table-cell">T7</view>
					<view class="table-cell">T8</view>
					<view class="table-cell">T9</view>
					<view class="table-cell">T10</view>
					<view class="table-cell">T11</view>
					<view class="table-cell">T12</view>
			</view>
			<view class="table-row">
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT1Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT2Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT3Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT4Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT5Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT6Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT7Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT8Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT9Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT10Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT11Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT12Set" /></view>		
			</view>
			<view class="table-row">
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT1Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT2Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT3Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT4Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT5Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT6Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT7Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT8Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT9Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT10Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT11Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.hotRunnerT12Actual" /></view>		
					
			</view>

			<view class="table-row table-header-row">
					<view class="table-cell">T13</view>
					<view class="table-cell">T14</view>
					<view class="table-cell">T15</view>
					<view class="table-cell">T16</view>
					<view class="table-cell">T17</view>
					<view class="table-cell">T18</view>
					<view class="table-cell">T19</view>
					<view class="table-cell">T20</view>
					<view class="table-cell">T21</view>
					<view class="table-cell">T22</view>
					<view class="table-cell">T23</view>
					<view class="table-cell">T24</view>
			</view>
			<view class="table-row">
					<view class="table-cell"><input type="number" v-model="model.subBarrelT13Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT14Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT15Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT16Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT17Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT18Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT19Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT20Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT21Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT22Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT23Set" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT24Set" /></view>	
			</view>
			<view class="table-row">
					<view class="table-cell"><input type="number" v-model="model.subBarrelT13Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT14Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT15Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT16Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT17Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT18Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT19Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT20Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT21Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT22Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT23Actual" /></view>
					<view class="table-cell"><input type="number" v-model="model.subBarrelT24Actual" /></view>	
			</view>
			
			<view class="table-row">
				<view class="table-cell">干燥温度1(℃)</view>
				<view class="table-cell"><input type="number" v-model="model.dryingTemp1"/></view>
			    <view class="table-cell">干燥时间1(小时)</view>
			    <view class="table-cell"><input type="number" v-model="model.dryingTime1"/></view>
			    <view class="table-cell">干燥温度2(℃)</view>
			    <view class="table-cell"><input type="number" v-model="model.dryingTemp2"/></view>
					<view class="table-cell">干燥时间2(小时)</view>
			    <view class="table-cell"><input type="number" v-model="model.dryingTime2"/></view>
			</view>
			
			<!-- 添加主射台射出参数 -->
			<view class="table-header">主射台注射参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">动作</view>
			    <view class="table-cell">位置</view>
			    <view class="table-cell">压力</view>
			    <view class="table-cell">速度</view>
			    <view class="table-cell">时间</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出一段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection1Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection1Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出二段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection2Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection2Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection2Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出三段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection3Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection3Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection3Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection3Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出四段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection4Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection4Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection4Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjection4Time"/></view>
			</view>
			<view class="table-row">
					<view class="table-cell">转换保压</view>
					<view class="table-cell"><input type="number" v-model="model.mainChangeoverHolding"/></view>
			</view>
			<!-- 添加主射台保压参数 -->
			<view class="table-header">主射台保压参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">动作</view>
			    <view class="table-cell">位置</view>
			    <view class="table-cell">压力</view>
			    <view class="table-cell">速度</view>
			    <view class="table-cell">时间</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压一段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding1Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding1Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压二段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding2Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding2Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding2Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压三段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding3Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding3Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding3Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainHolding3Time"/></view>
			</view>
			<view class="table-row">
					<view class="table-cell">保压方式</view>
			    <view class="table-cell"><input v-model="model.mainHoldingMethod"/></view>
			    <view class="table-cell">位置：0/时间：1</view>
					<view class="table-cell">射胶残留量(mm)</view>
			    <view class="table-cell"><input type="number" v-model="model.mainInjectionRemaining"/></view>
			</view>
			
			<!-- 添加主射台储料参数 -->
			<view class="table-header">主射台储料参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">动作</view>
			    <view class="table-cell">位置</view>
			    <view class="table-cell">压力</view>
			    <view class="table-cell">速度</view>
			    <view class="table-cell">背压</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">储料一段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing1Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing1Backpressure"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">储料二段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing2Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing2Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing2Backpressure"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">储料三段</view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing3Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing3Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing3Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizing3Backpressure"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射退</view>
			    <view class="table-cell"><input type="number" v-model="model.mainShotBack"/></view>
			    <view class="table-cell">储料终止位置(mm)</view>
			    <view class="table-cell"><input type="number" v-model="model.mainPlasticizingEndPosition"/></view>
			    
			</view>
			
			<!-- 添加主射台其他参数 -->
			<view class="table-header">主射台其他参数</view>
			<view class="table-row">
				<view class="table-cell">储前冷却时间(s)</view>
				<view class="table-cell"><input type="number" v-model="model.mainPreCoolingTime"/></view>
			    <view class="table-cell">储后冷却时间(s)</view>
			    <view class="table-cell"><input type="number" v-model="model.mainPostCoolingTime"/></view>
			    <view class="table-cell">再储料时间(s)</view>
			    <view class="table-cell"><input type="number" v-model="model.mainReplasticizingTime"/></view>
			    <view class="table-cell">冷却时间(s)</view>
			    <view class="table-cell"><input type="number" v-model="model.mainCoolingTime"/></view>
			</view>
			
			<!-- 添加副射台射出参数 -->
			<view class="table-header">副射台注射参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">动作</view>
			    <view class="table-cell">位置</view>
			    <view class="table-cell">压力</view>
			    <view class="table-cell">速度</view>
			    <view class="table-cell">时间</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出一段</view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection1Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection1Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出二段</view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection2Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection2Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection2Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出三段</view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection3Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection3Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection3Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection3Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射出四段</view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection4Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection4Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection4Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subInjection4Time"/></view>
			</view>
			<view class="table-row">
				<view class="table-cell">转换保压</view>
			  <view class="table-cell"><input type="number" v-model="model.subChangeoverHolding"/></view>
			</view>
			
	
			<!-- 添加副射台保压参数 -->
			<view class="table-header">副射台保压参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">动作</view>
			    <view class="table-cell">位置</view>
			    <view class="table-cell">压力</view>
			    <view class="table-cell">速度</view>
			    <view class="table-cell">时间</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压一段</view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding1Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding1Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压二段</view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding2Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding2Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding2Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压三段</view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding3Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding3Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding3Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subHolding3Time"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">保压方式</view>
			    <view class="table-cell"><input v-model="model.subHoldingMethod"/></view>
					<view class="table-cell">位置：0/时间：1</view>
			    <view class="table-cell">射胶残留量(mm)</view>
			    <view class="table-cell"><input type="number" v-model="model.subInjectionRemaining"/></view>
			</view>
			<!-- 添加副射台储料参数 -->
			<view class="table-header">副射台储料参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">动作</view>
			    <view class="table-cell">位置</view>
			    <view class="table-cell">压力</view>
			    <view class="table-cell">速度</view>
			    <view class="table-cell">背压</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">储料一段</view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing1Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing1Backpressure"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">储料二段</view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing2Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing2Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing2Backpressure"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">储料三段</view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing3Position"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing3Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing3Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizing3Backpressure"/></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">射退</view>
			    <view class="table-cell"><input type="number" v-model="model.subShotBack"/></view>
			    <view class="table-cell">储料终止位置(mm)</view>
			    <view class="table-cell"><input type="number" v-model="model.subPlasticizingEndPosition"/></view>
			    
			</view>
			
			<!-- 添加副射台其他参数 -->
			<view class="table-header">副射台其他参数</view>
			<view class="table-row">
					<view class="table-cell">储前冷却时间(s)</view>
					<view class="table-cell"><input type="number" v-model="model.subPreCoolingTime"/></view>
			    <view class="table-cell">储后冷却时间(s)</view>
			    <view class="table-cell"><input type="number" v-model="model.subPostCoolingTime"/></view>
			    <view class="table-cell">再储料时间(s)</view>
			    <view class="table-cell"><input type="number" v-model="model.subReplasticizingTime"/></view>
			    <view class="table-cell">冷却时间(s)</view>
			    <view class="table-cell"><input type="number" v-model="model.subCoolingTime"/></view>
			</view>

			<!-- 添加转芯动作参数 -->
			<view class="table-header">转芯动作参数</view>
			<view class="table-row">
			    <view class="table-cell">动作</view>
			    <!-- <view class="table-cell"><input v-model="model.coreAction"/></view> -->
			    <view class="table-cell">速度(rpm)</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.coreSpeedRpm"/></view> -->
			    <view class="table-cell">定位</view>
			    <!-- <view class="table-cell"><input v-model="model.corePositioning"/></view> -->
			    <view class="table-cell">定位进</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.corePositioningIn"/></view> -->
			    <view class="table-cell">定位退</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.corePositioningOut"/></view> -->
			</view>
			<view class="table-row">
			    <view class="table-cell">移入</view>
			    <view class="table-cell"></view>
					<view class="table-cell">压力</view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">移出</view>
			    <view class="table-cell"></view>
					<view class="table-cell">速度</view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">定位进限制时间</view>
			    <view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">定位进限制时间</view>
			    <view class="table-cell"></view>
			</view>
			
			
			<!-- 添加托模动作参数 -->
			<view class="table-header">托模动作参数</view>
			<view class="table-row">
			    <view class="table-cell">动作</view>
			    <!-- <view class="table-cell"><input v-model="model.ejectionAction"/></view> -->
			    <view class="table-cell">位置</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.ejectionPosition"/></view> -->
			    <view class="table-cell">压力</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.ejectionPressure"/></view> -->

			    <view class="table-cell">速度</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.ejectionSpeed"/></view> -->
			    <view class="table-cell">时间</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.ejectionTime"/></view> -->
			</view>
			<view class="table-row">
			    <view class="table-cell">托进1</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">托进2</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">托退1</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">托退2</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			
			
			<!-- 添加抽芯/绞牙动作参数 -->
			<view class="table-header">抽芯/绞牙</view>
			<view class="table-row">
			    <view class="table-cell">动作</view>
			    <!-- <view class="table-cell"><input v-model="model.corePullingAction"/></view> -->
			    <view class="table-cell">位置</view>
					<view class="table-cell">压力</view>
					<view class="table-cell">速度</view>
			    <!-- <view class="table-cell"><input type="number" v-model="model.corePullingSpeedRpm"/></view> -->
					<view class="table-cell">时间</view>
			</view>


			<view class="table-row">
			    <view class="table-cell">A进芯</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">A退芯</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">B进芯</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			<view class="table-row">
			    <view class="table-cell">B退芯</view>
			    <view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
					<view class="table-cell"></view>
			</view>
			
			<!-- 添加开模参数 -->
			<view class="table-header">开模参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">段数</view>
					<view class="table-cell">T1</view>
					<view class="table-cell">T2</view>
					<view class="table-cell">T3</view>
					<view class="table-cell">T4</view>
					<view class="table-cell">T5</view>
					<view class="table-cell">T6</view>
					<view class="table-cell">T7</view>
			</view>
			<view class="table-row">
			    <view class="table-cell">位置(mm)</view>
			    <view class="table-cell"><input type="number" v-model="model.moldOpeningT1Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT2Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT3Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT4Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT5Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT6Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT7Position"/></view>	
					
			</view>
			<view class="table-row">
			    <view class="table-cell">压力(bar)</view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.moldOpeningT2Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT3Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT4Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT5Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT6Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT7Pressure"/></view>
					
			</view>
			<view class="table-row">
					<view class="table-cell">速度(mm/s)</view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT1Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.moldOpeningT2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.moldOpeningT3Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT4Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT5Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT6Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldOpeningT7Speed"/></view>
			</view>
			
			
			<!-- 添加合模参数 -->
			<view class="table-header">合模参数</view>
			<view class="table-row table-header-row">
			    <view class="table-cell">段数</view>
					<view class="table-cell">T1</view>
					<view class="table-cell">T2</view>
					<view class="table-cell">T3</view>
					<view class="table-cell">T4</view>
					<view class="table-cell">T5</view>
					<view class="table-cell">T6</view>
					<view class="table-cell">T7</view>

			</view>
			<view class="table-row">				
			    <view class="table-cell">位置(mm)</view>
			    <view class="table-cell"><input type="number" v-model="model.moldClosingT1Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT2Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT3Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT4Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT5Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT6Position"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT7Position"/></view>	
			</view>
			<view class="table-row">
					<view class="table-cell">压力(bar)</view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT1Pressure"/></view>
			    <view class="table-cell"><input type="number" v-model="model.moldClosingT2Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT3Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT4Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT5Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT6Pressure"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT7Pressure"/></view>
					
					
			</view>
			<view class="table-row">
			    <view class="table-cell">速度(mm/s)</view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT1Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT2Speed"/></view>
			    <view class="table-cell"><input type="number" v-model="model.moldClosingT3Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT4Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT5Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT6Speed"/></view>
					<view class="table-cell"><input type="number" v-model="model.moldClosingT7Speed"/></view>
					
			</view>
			
			
			<!-- 公差控制 -->
			<view class="table-section">
				<view class="table-header">公差控制</view>
				<view class="table-row">
					<view class="table-cell">位置公差(±5mm)</view>
					<view class="table-cell"><input type="number" v-model="model.positionTolerance"/></view>
					<view class="table-cell">压力公差(±10bar)</view>
					<view class="table-cell"><input type="number" v-model="model.pressureTolerance"/></view>
					<view class="table-cell">速度公差(±5mm/s)</view>
					<view class="table-cell"><input type="number" v-model="model.speedTolerance"/></view>
					<view class="table-cell">时间公差(±2s)</view>
					<view class="table-cell"><input type="number" v-model="model.timeTolerance"/></view>
					<view class="table-cell">温度公差(±10℃)</view>
					<view class="table-cell"><input type="number" v-model="model.temperatureTolerance"/></view>
				</view>
			</view>
			
			<!-- 添加品质控制信息 -->
			<view class="table-section">
			    <view class="table-header">品质控制信息</view>
			    <view class="table-row">
			        <view class="table-cell" colspan="5">
			            <input v-model="model.qualityControlPoints1" style="width:100%"/>
			        </view>
							<view class="table-cell" colspan="5">
							    <input v-model="model.qualityControlPoints2" style="width:100%"/>
							</view>
			    </view>
				<view class="table-row">
				    <view class="table-cell" colspan="5">
				        <input v-model="model.qualityControlPoints2" style="width:100%"/>
				    </view>
						<view class="table-cell" colspan="5">
						    <input v-model="model.qualityControlPoints2" style="width:100%"/>
						</view>
				</view>
				<view class="table-row">
				    <view class="table-cell" colspan="5">
				        <input v-model="model.qualityControlPoints3" style="width:100%"/>
				    </view>
						<view class="table-cell" colspan="5">
						    <input v-model="model.qualityControlPoints2" style="width:100%"/>
						</view>
				</view>

			<!-- 其他参数区块类似... -->
			
			<!-- 添加系统信息 -->
			<view class="table-section">
			    <view class="table-header">系统信息</view>
					<view class="table-row">
						    <view class="table-cell">版本</view>
								<view class="table-cell">修订内容</view>
								<view class="table-cell">修订者</view>
								<view class="table-cell">修订日期</view>
								<view class="table-cell">编制人员</view>
								<view class="table-cell"><input v-model="model.creator"/></view>
						</view>
					    <view class="table-row">
					        <view class="table-cell" colspan="5">
					            <input v-model="model.version2" style="width:100%"/>
					        </view>
					        <view class="table-cell" colspan="5">
					            <input v-model="model.revisionContent" style="width:100%"/>
					        </view>
									<view class="table-cell"><input v-model="model.reviser"/></view>
									<view class="table-cell">
									    <input  fields="day" v-model="model.revisionDate"/>
									</view>
									<view class="table-cell">审核人员</view>
									<view class="table-cell"><input v-model="model.reviewer"/></view>
					    </view>
							<view class="table-row">
							  <view>表单编号：QP-003-03  版本：1.3</view>
							</view>
					</view>
					
			</view>

			<!-- 提交按钮 -->
			<view class="submit-section">
				<button class="cu-btn block bg-blue margin-tb-sm lg" @click="onSubmit" :disabled="loading">
					<text v-if="loading" class="cuIcon-loading2 cuIconfont-spin"></text>提交
				</button>
			</view>
		</view>
    </view>
</template>

<script>
    import myDate from '@/components/my-componets/my-date.vue'

    export default {
        name: "InjectionMoldingProcessForm",
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
                  queryById: "/degson/injectionMoldingProcess/queryById",
                  add: "/degson/injectionMoldingProcess/add",
                  edit: "/degson/injectionMoldingProcess/edit",
                },
            }
        },
        created(){
             this.initFormData();
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
                let myForm = {...this.model};
                this.loading = true;
                let url = myForm.id?this.url.edit:this.url.add;
				this.$http.post(url,myForm).then(res=>{
				   console.log("res",res)
				   this.loading = false
				   this.$Router.push({name:this.backRouteName})
				}).catch(()=>{
					this.loading = false
				});
            }
        }
    }
</script>
 
<style scoped>
.table-container {
    padding: 20rpx;
		font-size: 12rpx;
}

.table-section {
    /* margin-bottom: 10rpx; */
    /* border: 1px solid #828282; */
    border-radius: 3rpx;
}

.table-header {
    padding: 5rpx;
    font-weight: bold;
    border-bottom: 1px solid #7a7a7a;
		color: #25a8cf;
		font-size: 20rpx;
		text-align: center;
		/* border: 1px solid #828282; */
}

.table-subheader {
    background-color: #f9f9f9;
    padding: 15rpx 20rpx;
    font-weight: bold;
    border-bottom: 1px solid #bebebe;
		/* border: 1px solid #828282; */
}

.table-header-row {
    background-color: #f0f0f0;
    font-weight: bold;
}

.table-row {
    display: flex;
    border-right: 1px solid #838383;
		border-bottom: 1px solid #838383;
		border-left: 1px solid #838383;
}

.table-row:last-child {
    /* border-bottom: nopp'[]ne; */
}

.table-cell {
    flex: 1;
    /* padding-left: 15rpx; */
    border-right: 1px solid #838383;
    display: flex;
    align-items: center;
		justify-content: center;
    min-height: 28rpx;
}

.table-cell:last-child {
    border-right: none;
}

.table-cell input {
    width: 100%;
    border-radius: 2rpx;
    /* padding: 8rpx 12rpx; */
    font-size: 12rpx;
}

.submit-section {
    padding: 30rpx;
    text-align: center;
}
</style>