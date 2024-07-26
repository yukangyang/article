```html
<template>
	<div class="menu">
		<div class="menu-item">
			<div class="menu-item__undo" title="撤销(Ctrl+Z)" @click="instance.command.executeUndo()">
				<undo></undo>
			</div>
			<div class="menu-item__redo" title="重做(Ctrl+Y)" @click="instance.command.executeRedo()">
				<redo></redo>
			</div>
			<div class="menu-item__painter" title="格式刷(双击可连续使用)" @click="instance.command.executePainter()">
				<painter></painter>
			</div>
			<div class="menu-item__format" title="清除格式" @click="instance.command.executeFormat()">
				<format></format>
			</div>
		</div>
		<div class="menu-divider"></div>
		<div class="menu-item">
			<div class="menu-item__font" @click="fontClick">
				<span class="select" title="字体">微软雅黑</span>
				<div class="options" @click="fontChange($event)">
					<ul>
						<li data-family="Microsoft YaHei" style="font-family: 'Microsoft YaHei'">微软雅黑</li>
						<li data-family="宋体" style="font-family: '宋体'">宋体</li>
						<li data-family="黑体" style="font-family: '黑体'">黑体</li>
						<li data-family="仿宋" style="font-family: '仿宋'">仿宋</li>
						<li data-family="楷体" style="font-family: '楷体'">楷体</li>
						<li data-family="等线" style="font-family: '等线'">等线</li>
						<li data-family="华文琥珀" style="font-family: '华文琥珀'">华文琥珀</li>
						<li data-family="华文楷体" style="font-family: '华文楷体'">华文楷体</li>
						<li data-family="华文隶书" style="font-family: '华文隶书'">华文隶书</li>
						<li data-family="华文新魏" style="font-family: '华文新魏'">华文新魏</li>
						<li data-family="华文行楷" style="font-family: '华文行楷'">华文行楷</li>
						<li data-family="华文中宋" style="font-family: '华文中宋'">华文中宋</li>
						<li data-family="华文彩云" style="font-family: '华文彩云'">华文彩云</li>
						<li data-family="Arial" style="font-family: 'Arial'">Arial</li>
						<li data-family="Segoe UI" style="font-family: 'Segoe UI'">Segoe UI</li>
						<li data-family="Ink Free" style="font-family: 'Ink Free'">Ink Free</li>
						<li data-family="Fantasy" style="font-family: 'Fantasy'">Fantasy</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__size" @click="sizeClick">
				<span class="select" title="字体">小四</span>
				<div class="options" @click="sizeChange($event)">
					<ul>
						<li data-size="56">初号</li>
						<li data-size="48">小初</li>
						<li data-size="34">一号</li>
						<li data-size="32">小一</li>
						<li data-size="29">二号</li>
						<li data-size="24">小二</li>
						<li data-size="21">三号</li>
						<li data-size="20">小三</li>
						<li data-size="18">四号</li>
						<li data-size="16">小四</li>
						<li data-size="14">五号</li>
						<li data-size="12">小五</li>
						<li data-size="10">六号</li>
						<li data-size="8">小六</li>
						<li data-size="7">七号</li>
						<li data-size="6">八号</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__size-add" @click="sizeAddClick">
				<UiwSizeAdd></UiwSizeAdd>
			</div>
			<div class="menu-item__size-minus" @click="sizeMinusClick">
				<UiwSizeMinus></UiwSizeMinus>
			</div>
			<div class="menu-item__bold" @click="executeBold">
				<UiwBlod></UiwBlod>
			</div>
			<div class="menu-item__italic" @click="executeItalic">
				<UiwItalic></UiwItalic>
			</div>
			<div class="menu-item__underline" @click="underlineClick">
				<UiwUnderLine class="w-[30px]"></UiwUnderLine>
				<span class="select"></span>
				<div class="options">
					<ul>
						<li
							data-decoration-style="solid"
							v-for="item in underlineList"
							:key="item.value"
							@click="underlineChange(item.value)"
						>
							<component :is="item.icon"></component>
						</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__strikeout" title="删除线(Ctrl+Shift+X)" @click="executeStrikeout">
				<UiwStrikeOut></UiwStrikeOut>
			</div>
			<div class="menu-item__superscript" @click="executeSuperscript" title="上标">
				<UiwSuperScript class="w-[16px]"></UiwSuperScript>
			</div>
			<div class="menu-item__subscript" @click="executeSubscript">
				<UiwSubScript class="w-[16px]"></UiwSubScript>
			</div>
			<div class="menu-item__color" title="字体颜色" @click="colorClick">
				<UiwColor></UiwColor>
				<span></span>
				<input type="color" id="color" />
			</div>
			<div class="menu-item__highlight" title="高亮" @click="highlightClick">
				<UiwHighLight></UiwHighLight>
				<span></span>
				<input type="color" id="highlight" />
			</div>
		</div>
		<div class="menu-divider"></div>
		<div class="menu-item">
			<div class="menu-item__title" @click="titleClick">
				<UiwWordTitle></UiwWordTitle>
				<span class="select" title="切换标题">正文</span>
				<div class="options" @click="titleChange($event)">
					<ul>
						<li style="font-size: 16px">正文</li>
						<li data-level="first" style="font-size: 26px">标题1</li>
						<li data-level="second" style="font-size: 24px">标题2</li>
						<li data-level="third" style="font-size: 22px">标题3</li>
						<li data-level="fourth" style="font-size: 20px">标题4</li>
						<li data-level="fifth" style="font-size: 18px">标题5</li>
						<li data-level="sixth" style="font-size: 16px">标题6</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__left" @click="executeLeft" :title="`左对齐(${isApple ? '⌘' : 'Ctrl'}+L)`">
				<UiwWordLeft></UiwWordLeft>
			</div>
			<div class="menu-item__center" @click="executeCenter" :title="`居中对齐(${isApple ? '⌘' : 'Ctrl'}+E)`">
				<UiwWordCenter></UiwWordCenter>
			</div>
			<div class="menu-item__right" @click="executeRight" :title="`右对齐(${isApple ? '⌘' : 'Ctrl'}+R)`">
				<UiwWordRight></UiwWordRight>
			</div>
			<div class="menu-item__alignment" @click="executeAlignment" :title="`两端对齐(${isApple ? '⌘' : 'Ctrl'}+J)`">
				<UiwWordAlignment></UiwWordAlignment>
			</div>
			<div class="menu-item__row-margin" @click="rowMarginClick" title="行间距">
				<UiwWordRowMargin></UiwWordRowMargin>
				<div class="options" @click="rowMarginChange($event)">
					<ul>
						<li data-rowmargin="1">1</li>
						<li data-rowmargin="1.25">1.25</li>
						<li data-rowmargin="1.5">1.5</li>
						<li data-rowmargin="1.75">1.75</li>
						<li data-rowmargin="2">2</li>
						<li data-rowmargin="2.5">2.5</li>
						<li data-rowmargin="3">3</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__list" @click="listClick" title="列表">
				<UiwWordList></UiwWordList>
				<div class="options" @click="listChange($event)">
					<ul>
						<li>
							<label>取消列表</label>
						</li>
						<li data-list-type="ol" data-list-style="decimal">
							<label>有序列表：</label>
							<ol>
								<li>________</li>
							</ol>
						</li>
						<li data-list-type="ul" data-list-style="checkbox">
							<label>复选框列表：</label>
							<ul style="list-style-type: '☑️ '">
								<li>________</li>
							</ul>
						</li>
						<li data-list-type="ul" data-list-style="disc">
							<label>实心圆点列表：</label>
							<ul style="list-style-type: disc">
								<li>________</li>
							</ul>
						</li>
						<li data-list-type="ul" data-list-style="circle">
							<label>空心圆点列表：</label>
							<ul style="list-style-type: circle">
								<li>________</li>
							</ul>
						</li>
						<li data-list-type="ul" data-list-style="square">
							<label>空心方块列表：</label>
							<ul style="list-style-type: square">
								<li>________</li>
							</ul>
						</li>
					</ul>
				</div>
			</div>
		</div>
		<div class="menu-divider"></div>
		<div class="menu-item">
			<div class="menu-item__table" title="表格">
				<UiwWordTable @click="tableClick"></UiwWordTable>
			</div>
			<div class="menu-item__table__collapse">
				<div class="table-close" @click="recoveryTable">×</div>
				<div class="table-title">
					<span class="table-select">插入</span>
					<span>表格</span>
				</div>
				<div class="table-panel" @mousemove="tableMouseMove($event)" @click.prevent="tableRowCellClick"></div>
			</div>
			<div class="menu-item__image" title="图片" @click="imageClick">
				<UiwWordImage class="w-[16px]"></UiwWordImage>
				<input type="file" id="image" accept=".png, .jpg, .jpeg, .svg, .gif" />
			</div>
			<div
				class="menu-item__hyperlink"
				title="超链接"
				@click="() => ((hyperlinkModalVisible = true), (hyperlink.hyperlinkUrl = instance.command.getRangeText()))"
			>
				<UiwWordHyperlink></UiwWordHyperlink>
			</div>
			<div class="menu-item__separator" title="分割线" @click="separatorClick">
				<UiwSeparator></UiwSeparator>
				<div class="options">
					<ul>
						<li v-for="item in separatorList" :key="item.value" @click="separatorChange(item.value)">
							<component :is="item.icon"></component>
						</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__watermark" title="水印(添加、删除)" @click="watermarkClick">
				<UiwWaterMark></UiwWaterMark>
				<div class="options">
					<ul>
						<li data-menu="add" @click="watermarkModalVisible = true">添加水印</li>
						<li data-menu="delete" @click="instance.command.executeDeleteWatermark()">删除水印</li>
					</ul>
				</div>
			</div>
			<div class="menu-item__codeblock" title="代码块" @click="codeBoxVisible = true">
				<UiwCodeBlock></UiwCodeBlock>
			</div>
			<div class="menu-item__page-break" title="分页符" @click="instance.command.executePageBreak()">
				<UiwPageBreak class="w-[16px]"></UiwPageBreak>
			</div>
			<div class="menu-item__control" title="控件" @click="controlClick">
				<UiwControl></UiwControl>
				<div class="options">
					<ul>
						<li data-control="text" @click="() => ((controlbox.type = ControlType.TEXT), (controlModalVisible = true))">
							文本
						</li>
						<li
							data-control="select"
							@click="() => ((controlbox.type = ControlType.SELECT), (controlModalVisible = true))"
						>
							列举
						</li>
						<li
							data-control="checkbox"
							@click="() => ((controlbox.type = ControlType.CHECKBOX), (controlModalVisible = true))"
						>
							复选框
						</li>
					</ul>
				</div>
			</div>
			<div
				class="menu-item__checkbox"
				title="复选框"
				@click="
					instance.command.executeInsertElementList([
						{
							type: ElementType.CHECKBOX,
							checkbox: {
								value: false
							},
							value: ''
						}
					])
				"
			>
				<UiwCheckBox class="w-[16px]"></UiwCheckBox>
			</div>
			<div class="menu-item__latex" title="LateX" @click="latexVisible = true">
				<UiwLateX></UiwLateX>
			</div>
			<div class="menu-item__date" @click="dateClick" title="日期">
				<UiwWordDate></UiwWordDate>
				<div class="options" @click="dateChange($event)">
					<ul>
						<li data-format="yyyy-MM-dd"></li>
						<li data-format="yyyy-MM-dd hh:mm:ss"></li>
					</ul>
				</div>
			</div>
			<div class="menu-item__block" title="内容块" @click="contentBlockModalVisible = true">
				<UiwWordBlock></UiwWordBlock>
			</div>
		</div>
		<div class="menu-divider"></div>
		<div class="menu-item">
			<div
				class="menu-item__search"
				data-menu="search"
				:title="`搜索与替换(${isApple ? '⌘' : 'Ctrl'}+F)`"
				@click="searchClick"
			>
				<UiwWordSearch></UiwWordSearch>
			</div>
			<div class="menu-item__search__collapse" data-menu="search">
				<div class="menu-item__search__collapse__search">
					<input type="text" />
					<label class="search-result"></label>
					<div class="arrow-left">
						<UiwWordSearchArrowLeft></UiwWordSearchArrowLeft>
					</div>
					<div class="arrow-right">
						<UiwWordSearchArrowRight></UiwWordSearchArrowRight>
					</div>
					<span>×</span>
				</div>
				<div class="menu-item__search__collapse__replace">
					<input type="text" />
					<button>替换</button>
				</div>
			</div>
			<div
				class="menu-item__print"
				data-menu="print"
				:title="`打印(${isApple ? '⌘' : 'Ctrl'}+P)`"
				@click="instance.command.executePrint()"
			>
				<UiwWordPrint></UiwWordPrint>
			</div>
		</div>
	</div>
	<div class="catalog" editor-component="catalog">
		<div class="catalog__header">
			<span>目录</span>
			<div class="catalog__header__close" @click="catalogClose">
				<UiwCataLogClose></UiwCataLogClose>
			</div>
		</div>
		<div class="catalog__main"></div>
	</div>
	<div class="canvas-editor mx-auto my-[80px] bg-[#f2f4f7]"></div>
	<div class="footer" editor-component="footer">
		<div>
			<div class="catalog-mode" title="目录" @click="catelogClick">
				<UiwCateLog class="mr-[5px]"></UiwCateLog>
			</div>
			<div class="page-mode" title="页面模式(分页、连页)" @click="pageModeClick">
				<UiwPageMode class="mr-[5px]"></UiwPageMode>
				<div class="options" @click="pageModeChange($event)">
					<ul>
						<li data-page-mode="paging" class="active">分页</li>
						<li data-page-mode="continuity">连页</li>
					</ul>
				</div>
			</div>
			<span>可见页码：<span class="page-no-list">1</span></span>
			<span>页面：<span class="page-no">1</span>/<span class="page-size">1</span></span>
			<span>字数：<span class="word-count">0</span></span>
		</div>
		<div class="editor-mode" title="编辑模式(编辑、清洁、只读、表单)" @click="editorModeClick">编辑模式</div>
		<div>
			<div class="page-scale-minus" title="缩小(Ctrl+-)" @click="instance.command.executePageScaleMinus()">
				<UiwPageScaleMinus></UiwPageScaleMinus>
			</div>
			<span
				class="page-scale-percentage"
				title="显示比例(点击可复原Ctrl+0)"
				@click="instance.command.executePageScaleRecovery()"
				>100%</span
			>
			<div class="page-scale-add" title="放大(Ctrl+=)" @click="instance.command.executePageScaleAdd()">
				<UiwPageScaleAdd></UiwPageScaleAdd>
			</div>
			<div class="paper-size" title="纸张类型" @click="paperTypeClick">
				<UiwPageSize></UiwPageSize>
				<div class="options" @click="paperTypeChange($event)">
					<ul>
						<li data-paper-size="794*1123" class="active">A4</li>
						<li data-paper-size="1593*2251">A2</li>
						<li data-paper-size="1125*1593">A3</li>
						<li data-paper-size="565*796">A5</li>
						<li data-paper-size="412*488">5号信封</li>
						<li data-paper-size="450*866">6号信封</li>
						<li data-paper-size="609*862">7号信封</li>
						<li data-paper-size="862*1221">9号信封</li>
						<li data-paper-size="813*1266">法律用纸</li>
						<li data-paper-size="813*1054">信纸</li>
					</ul>
				</div>
			</div>
			<div class="paper-direction" title="纸张方向" @click="paperDirectionClick">
				<UiwPaperDirection class="w-[16px]"></UiwPaperDirection>
				<div class="options" @click="paperDirectionChange($event)">
					<ul>
						<li data-paper-direction="vertical" class="active">纵向</li>
						<li data-paper-direction="horizontal">横向</li>
					</ul>
				</div>
			</div>
			<div class="paper-margin" title="页边距" @click="pageMarginClick">
				<UiwPaperMargin></UiwPaperMargin>
			</div>
			<div class="fullscreen" title="全屏显示" @click="fullScreenClick">
				<UiwRequestFullscreen v-if="!isFullScreen"></UiwRequestFullscreen>
				<UiwWordExitFullScreen v-else></UiwWordExitFullScreen>
			</div>
			<div class="editor-option" title="编辑器设置" @click="editorOptionClick">
				<UiwWordOption></UiwWordOption>
			</div>
		</div>
	</div>
	<input type="file" name="file-docx" id="file-docx" accept=".docx" style="display: none" />
	<!-- #region 超链接-->
	<DragModal
		:border="false"
		:visible="hyperlinkModalVisible"
		@close="() => (hyperlinkModalVisible = false)"
		:width="500"
		title="超链接"
	>
		<a-form :model="hyperlink" ref="hyperlinkFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-form-item label="文本" :rules="[{ required: true }]" name="hyperlinkUrl">
				<a-input v-model:value="hyperlink.hyperlinkUrl" placeholder="文本" />
			</a-form-item>
			<a-form-item label="链接" :rules="[{ required: true }]" name="hyperlinkText">
				<a-input v-model:value="hyperlink.hyperlinkText" placeholder="链接" />
			</a-form-item>
		</a-form>
		<template #footer>
			<a-button @click="() => (hyperlinkModalVisible = false)">取消</a-button>
			<a-button type="primary" @click="hyperlinkClick">确定</a-button>
		</template>
	</DragModal>
	<!-- #endregion -->
	<!-- #region 水印-->
	<DragModal
		:border="false"
		:visible="watermarkModalVisible"
		@close="() => (watermarkModalVisible = false)"
		:width="500"
		title="水印"
	>
		<a-form :model="watermark" ref="watermarkFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-form-item label="内容" :rules="[{ required: true }]" name="content">
				<a-input v-model:value="watermark.content" placeholder="请输入内容" />
			</a-form-item>
			<a-form-item label="颜色" :rules="[{ required: true }]" name="color">
				<color-picker format="hex" v-model:pureColor="watermark.color" />
			</a-form-item>
			<a-form-item label="字体大小" :rules="[{ required: true }]" name="fontSize">
				<a-input-number v-model:value="watermark.fontSize" :defaultValue="16" placeholder="字体大小" />
			</a-form-item>
		</a-form>
		<template #footer>
			<a-button @click="() => (watermarkModalVisible = false)">取消</a-button>
			<a-button type="primary" @click="watermarkConfirm">确定</a-button>
		</template>
	</DragModal>
	<!-- #endregion -->
	<!-- #region 代码块-->
	<DragModal
		:border="false"
		:visible="codeBoxVisible"
		@close="() => (codeBoxVisible = false)"
		:width="500"
		title="代码块"
	>
		<a-form :model="codeBox" ref="codeBoxFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-textarea v-model:value="codeBox.content" placeholder="请输入内容" />
		</a-form>
		<template #footer>
			<a-button @click="() => (codeBoxVisible = false)">取消</a-button>
			<a-button type="primary" @click="codeBoxConfirm">确定</a-button>
		</template>
	</DragModal>
	<!-- #endregion -->
	<!-- #region LateX-->
	<DragModal :border="false" :visible="latexVisible" @close="() => (latexVisible = false)" :width="500" title="LaTeX">
		<a-form :model="latexBox" ref="latexBoxFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-textarea v-model:value="latexBox.content" placeholder="请输入内容" />
		</a-form>
		<template #footer>
			<a-button @click="() => (latexVisible = false)">取消</a-button>
			<a-button type="primary" @click="latexBoxConfirm">确定</a-button>
		</template>
	</DragModal>
	<!-- #endregion -->
	<!-- #region 控件-->
	<DragModal
		:border="false"
		:visible="controlModalVisible"
		@close="() => (controlModalVisible = false)"
		:width="500"
		:title="controlFlatList[controlbox.type]"
	>
		<a-form :model="controlbox" ref="controlboxFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-form-item
				v-if="controlbox.type === ControlType.TEXT || controlbox.type === ControlType.SELECT"
				label="占位符"
				:rules="[{ required: true }]"
				name="placeholder"
			>
				<a-input v-model:value="controlbox.placeholder" placeholder="请输入占位符" />
			</a-form-item>
			<a-form-item label="默认值" name="default">
				<a-input
					v-model:value="controlbox.default"
					:placeholder="
						controlbox.type === ControlType.CHECKBOX ? '请输入默认值，多个值以英文逗号分割' : '请输入默认值'
					"
				/>
			</a-form-item>
			<a-form-item v-if="controlbox.type !== ControlType.TEXT" :rules="[{ required: true }]" label="值集" name="list">
				<a-textarea v-model:value="controlbox.list" />
			</a-form-item>
		</a-form>
		<template #footer>
			<a-button @click="() => (controlModalVisible = false)">取消</a-button>
			<a-button type="primary" @click="controlboxConfirm">确定</a-button>
		</template>
	</DragModal>
	<!-- #endregion -->
	<!-- #region 内容块-->
	<DragModal
		:border="false"
		:visible="contentBlockModalVisible"
		@close="() => (contentBlockModalVisible = false)"
		:width="500"
		title="内容块"
	>
		<a-form :model="contentBlock" ref="contentBlockFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-form-item label="类型" :rules="[{ required: true }]" name="type">
				<a-select v-model:value="contentBlock.type">
					<a-select-option value="iframe">网址</a-select-option>
					<a-select-option value="video">视频</a-select-option>
				</a-select>
			</a-form-item>
			<a-form-item label="宽度" name="width">
				<a-input v-model:value="contentBlock.width" placeholder="请输入宽度(默认页面内宽度)" />
			</a-form-item>
			<a-form-item label="高度" name="hight" :rules="[{ required: true }]">
				<a-input v-model:value="contentBlock.hight" placeholder="请输入高度" />
			</a-form-item>
			<a-form-item label="地址" name="url">
				<a-input v-model:value="contentBlock.url" placeholder="请输入地址" />
			</a-form-item>
			<a-form-item label="HTML" name="html">
				<a-textarea v-model:value="contentBlock.html" placeholder="请输入HTML代码(仅网址类型有效)" />
			</a-form-item>
		</a-form>
		<template #footer>
			<a-button @click="() => (contentBlockModalVisible = false)">取消</a-button>
			<a-button type="primary" @click="contentBlockConfirm">确定</a-button>
		</template>
	</DragModal>
	<!-- #endregion -->
	<DragModal
		:border="false"
		:visible="pageMarginVisible"
		@close="() => (pageMarginVisible = false)"
		:width="500"
		title="页边距"
	>
		<a-form :model="pageMargin" ref="pageMarginFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-form-item label="上边距" name="top" :rules="[{ required: true }]">
				<a-input v-model:value="pageMargin.top" placeholder="请输入上边距" />
			</a-form-item>
			<a-form-item label="下边距" name="bottom" :rules="[{ required: true }]">
				<a-input v-model:value="pageMargin.bottom" placeholder="请输入下边距" />
			</a-form-item>
			<a-form-item label="左边距" name="left" :rules="[{ required: true }]">
				<a-input v-model:value="pageMargin.left" placeholder="请输入左边距" />
			</a-form-item>
			<a-form-item label="右边距" name="right" :rules="[{ required: true }]">
				<a-input v-model:value="pageMargin.right" placeholder="请输入右边距" />
			</a-form-item>
		</a-form>
		<template #footer>
			<a-button @click="() => (pageMarginVisible = false)">取消</a-button>
			<a-button type="primary" @click="pageMarginConfirm">确定</a-button>
		</template>
	</DragModal>
	<DragModal
		:border="false"
		:visible="editorOptionVisible"
		@close="() => (editorOptionVisible = false)"
		:width="500"
		title="编辑器配置"
	>
		<a-form :model="editorOption" ref="editorOptionFormRef" :labelCol="{ style: 'width: 80px' }">
			<a-form-item label="编辑器配置" name="content" :rules="[{ required: true }]">
				<a-textarea v-model:value="editorOption.content" placeholder="请输入编辑器配置" />
			</a-form-item>
		</a-form>
		<template #footer>
			<a-button @click="() => (editorOptionVisible = false)">取消</a-button>
			<a-button type="primary" @click="editorOptionConfirm">确定</a-button>
		</template>
	</DragModal>
	<a-modal v-model:open="docModalVisible" title="文档设置" @ok="handleOk">
		<a-row :gutter="24">
			<a-col :span="6"> 文档标题： </a-col>
			<a-col :span="18">
				<a-input v-model:value="formData.title" placeholder="文档标题" />
			</a-col>
		</a-row>
		<a-row :gutter="24" style="margin-top: 10px">
			<a-col :span="6"> 参与人员： </a-col>
			<a-col :span="18">
				<a-input v-model:value="formData.userIds" placeholder="参与人" />
			</a-col>
		</a-row>
	</a-modal>
</template>

<script setup>
	import Editor, { EditorMode, ElementType, RowFlex, splitText, ControlType, BlockType } from '@hufe921/canvas-editor'
	import barcode1DPlugin from '@hufe921/canvas-editor-plugin-barcode1d'
	import barcode2DPlugin from '@hufe921/canvas-editor-plugin-barcode2d'
	import codeblockPlugin from '@hufe921/canvas-editor-plugin-codeblock'
	import docxPlugin from '@hufe921/canvas-editor-plugin-docx'
	import floatingToolbarPlugin from '@hufe921/canvas-editor-plugin-floating-toolbar'
	import { ColorPicker } from 'vue3-colorpicker'
	import 'vue3-colorpicker/style.css'
	import { debounce } from 'lodash-es'
	import appDocWordApi from '@/api/app/appDocWordApi'
	import appDocItemApi from '@/api/app/appDocItemApi'
	import { useRoute } from 'vue-router'
	let isCatalogShow = true
	const isFullScreen = ref(false)
	const instance = ref(null)
	const docModalVisible = ref(false)
	const tableCellList = ref([])
	const colIndex = ref(0)
	const rowIndex = ref(0)
	const hyperlink = ref({})
	const codeBox = ref({})
	const watermark = ref({})
	const latexBox = ref({})
	const controlbox = ref({})
	const pageMargin = ref({})
	const editorOption = ref({})
	const codeBoxFormRef = ref()
	const hyperlinkFormRef = ref()
	const watermarkFormRef = ref()
	const latexBoxFormRef = ref()
	const controlboxFormRef = ref()
	const contentBlockFormRef = ref()
	const pageMarginFormRef = ref()
	const editorOptionFormRef = ref()
	const contentBlock = ref({})
	const isApple = typeof navigator !== 'undefined' && /Mac OS X/.test(navigator.userAgent)
	const hyperlinkModalVisible = ref(false)
	const watermarkModalVisible = ref(false)
	const codeBoxVisible = ref(false)
	const latexVisible = ref(false)
	const controlModalVisible = ref(false)
	const contentBlockModalVisible = ref(false)
	const pageMarginVisible = ref(false)
	const editorOptionVisible = ref(false)
	const formData = ref({
		docId: '',
		header: '',
		main: '',
		footer: ''
	})

	const Route = useRoute()
	//分割线列表
	const separatorList = [
		{
			icon: 'UiwLineSingle',
			value: '0,0'
		},
		{
			icon: 'UiwLineDot',
			value: '1,1'
		},
		{
			icon: 'UiwlineDashSmallGap',
			value: '3,1'
		},
		{
			icon: 'UiwlineDashLargeGap',
			value: '4,4'
		},
		{
			icon: 'UiwLineDashDot',
			value: '7,3,3,3'
		},
		{
			icon: 'UiwlineDashDotDot',
			value: '6,2,2,2,2,2'
		}
	]

	//underLine
	const underlineList = [
		{
			icon: 'UiwLineSingle',
			value: ' solid'
		},
		{
			icon: 'UiwLineDouble',
			value: 'double'
		},
		{
			icon: 'UiwLineDashed',
			value: 'dashed'
		},

		{
			icon: 'UiwLineDotted',
			value: 'dotted'
		},
		{
			icon: 'UiwLineWavy',
			value: 'wavy'
		}
	]

	//controlFlat
	const controlFlatList = {
		text: '文本控件',
		select: '列举控件',
		checkbox: '复选框控件'
	}

	const docId = ref('')

	const getAppWordDetail = (docId) => {
		 appDocWordApi.appDocWordDetail({ id: docId }).then((res) => {
			 console.log(res)
			instance.value.command.executeSetHTML({
				header: res.appDocItem.header,
				main: res.appDocItem.main,
				footer: res.appDocItem.footer
			})
			formData.value = {
				title: res.title,
				userIds: res.userIds,
				docId: res.id
			}
		})
	}

	onMounted(() => {
		docId.value = Route.query.id

		let app = document.querySelector('#app')
		app.style.backgroundColor = '#f2f4f7'
		app.style.overflow = 'scroll'
		instance.value = new Editor(
			document.querySelector('.canvas-editor'),
			{
				header: [
					{
						value: '标题',
						type: 'text',
						bold: true,
						size: 20,
						color: '#000000',
						highlight: '',
						italic: false,
						underline: false,
						strikeout: false,
						rowFlex: 'left',
						rowMargin: 1,
						letterSpacing: 10,
						groupIds: [],
						conceptId: '',
						colgroup: {
							LEFT: 'left'
						}
					}
				],
				main: [
					{
						value: '请开始你的表演'
					}
				],
				footer: [
					{
						value: '脚注',
						type: 'text',
						bold: true,
						size: 20,
						color: '#000000',
						highlight: '',
						italic: false,
						underline: false,
						strikeout: false,
						rowFlex: 'left',
						rowMargin: 1,
						letterSpacing: 10,
						groupIds: [],
						conceptId: '',
						colgroup: {
							LEFT: 'left'
						}
					}
				]
			},
			{
				id: 'canvas-editor',
				type: {
					TEXT: 'text',
					IMAGE: 'image',
					TABLE: 'table',
					HYPERLINK: 'hyperlink',
					SUPERSCRIPT: 'superscript',
					SUBSCRIPT: 'subscript',
					SEPARATOR: 'separator',
					PAGE_BREAK: 'pageBreak',
					CONTROL: 'control',
					CHECKBOX: 'checkbox',
					LATEX: 'latex',
					TAB: 'tab',
					DATE: 'date',
					BLOCK: 'block'
				},
				value: 'Hello World',
				valueList: [],
				// 样式
				font: 'Arial',
				size: 16,
				// width: 100,
				// height: 100,
				bold: false,
				color: '#000000',
				highlight: '',
				italic: false,
				underline: false,
				strikeout: false,
				rowFlex: {
					LEFT: 'left',
					CENTER: 'center',
					RIGHT: 'right',
					ALIGNMENT: 'alignment'
				},
				rowMargin: 20,
				letterSpacing: 10,
				// 组信息-可用于批注等其他成组使用场景
				groupIds: [],
				// 表格
				conceptId: '',
				colgroup: {
					width: 200
				},
				trList: {
					height: 200,
					tdList: {
						colspan: 20,
						rowspan: 20
					}
				}
			}
		)

		if (docId.value) {
			getAppWordDetail(docId.value)
		}

		instance.value.use(floatingToolbarPlugin)
		instance.value.use(barcode1DPlugin)
		instance.value.use(barcode2DPlugin)
		instance.value.use(codeblockPlugin)
		instance.value.use(docxPlugin)

		instance.value.register.contextMenuList([
			{
				name: '导出文档',
				when: (payload) => true,
				callback: (command) => {
					command.executeExportDocx({
						fileName: formData.value.title
					})
				}
			},
			{
				name: '导入文档',
				when: (payload) => true,
				callback: (command) => {
					fileInput.click()
				}
			}
		])
		const fileInput = document.querySelector('#file-docx')
		fileInput.onchange = () => {
			const file = fileInput?.files?.[0]
			if (!file) return
			const reader = new FileReader()
			reader.onload = (event) => {
				const buffer = event?.target?.result
				if (buffer instanceof ArrayBuffer) {
					instance.value.command.executeImportDocx({
						arrayBuffer: buffer
					})
				}
				fileInput.value = ''
			}
			reader.readAsArrayBuffer(file)
		}
		const colorDom = document.querySelector('.menu-item__color')
		const colorSpanDom = colorDom.querySelector('span')
		const colorControlDom = document.querySelector('#color')
		const highlightDom = document.querySelector('.menu-item__highlight')
		const highlightControlDom = document.querySelector('#highlight')
		const highlightSpanDom = highlightDom.querySelector('span')
		const subscriptDom = document.querySelector('.menu-item__subscript')
		const superscriptDom = document.querySelector('.menu-item__superscript')
		const separatorDom = document.querySelector('.menu-item__separator')
		const separatorOptionDom = separatorDom.querySelector('.options')

		const fontDom = document.querySelector('.menu-item__font')
		const fontSelectDom = fontDom.querySelector('.select')
		const fontOptionDom = fontDom.querySelector('.options')

		const sizeSetDom = document.querySelector('.menu-item__size')
		const sizeSelectDom = sizeSetDom.querySelector('.select')
		const sizeOptionDom = sizeSetDom.querySelector('.options')

		const boldDom = document.querySelector('.menu-item__bold')
		const italicDom = document.querySelector('.menu-item__italic')
		const underlineDom = document.querySelector('.menu-item__underline')
		const strikeoutDom = document.querySelector('.menu-item__strikeout')

		const leftDom = document.querySelector('.menu-item__left')
		const centerDom = document.querySelector('.menu-item__center')
		const rightDom = document.querySelector('.menu-item__right')
		const alignmentDom = document.querySelector('.menu-item__alignment')
		const rowMarginDom = document.querySelector('.menu-item__row-margin')
		const rowOptionDom = rowMarginDom.querySelector('.options')
		const undoDom = document.querySelector('.menu-item__undo')
		const redoDom = document.querySelector('.menu-item__redo')
		const painterDom = document.querySelector('.menu-item__painter')

		const titleDom = document.querySelector('.menu-item__title')
		const titleSelectDom = titleDom.querySelector('.select')
		const titleOptionDom = titleDom.querySelector('.options')

		instance.value.listener.visiblePageNoListChange = function (payload) {
			const text = payload.map((i) => i + 1).join('、')
			document.querySelector('.page-no-list').innerText = text
		}

		instance.value.listener.pageSizeChange = function (payload) {
			document.querySelector('.page-size').innerText = `${payload}`
		}

		instance.value.listener.intersectionPageNoChange = function (payload) {
			document.querySelector('.page-no').innerText = `${payload + 1}`
		}

		instance.value.listener.pageScaleChange = function (payload) {
			document.querySelector('.page-scale-percentage').innerText = `${Math.floor(payload * 10 * 10)}%`
		}

		instance.value.listener.contentChange = debounce(handleContentChange, 200)
		instance.value.eventBus.on('rangeStyleChange', (payload) => {
			if (payload.color) {
				colorDom.classList.add('active')
				colorControlDom.value = payload.color
				colorSpanDom.style.backgroundColor = payload.color
			} else {
				colorDom.classList.remove('active')
				colorControlDom.value = '#000000'
				colorSpanDom.style.backgroundColor = '#000000'
			}
			if (payload.highlight) {
				highlightDom.classList.add('active')
				highlightControlDom.value = payload.highlight
				highlightSpanDom.style.backgroundColor = payload.highlight
			} else {
				highlightDom.classList.remove('active')
				highlightControlDom.value = '#ffff00'
				highlightSpanDom.style.backgroundColor = '#ffff00'
			}

			// 控件类型
			payload.type === ElementType.SUBSCRIPT
				? subscriptDom.classList.add('active')
				: subscriptDom.classList.remove('active')
			payload.type === ElementType.SUPERSCRIPT
				? superscriptDom.classList.add('active')
				: superscriptDom.classList.remove('active')
			payload.type === ElementType.SEPARATOR
				? separatorDom.classList.add('active')
				: separatorDom.classList.remove('active')
			separatorOptionDom.querySelectorAll('li').forEach((li) => li.classList.remove('active'))
			if (payload.type === ElementType.SEPARATOR) {
				const separator = payload.dashArray.join(',') || '0,0'
				const curSeparatorDom = separatorOptionDom.querySelector(`[data-separator='${separator}']`)
				if (curSeparatorDom) {
					curSeparatorDom.classList.add('active')
				}
			}

			// 富文本
			fontOptionDom.querySelectorAll('li').forEach((li) => li.classList.remove('active'))
			const curFontDom = fontOptionDom.querySelector(`[data-family='${payload.font}']`)
			if (curFontDom) {
				fontSelectDom.innerText = curFontDom.innerText
				fontSelectDom.style.fontFamily = payload.font
				curFontDom.classList.add('active')
			}
			sizeOptionDom.querySelectorAll('li').forEach((li) => li.classList.remove('active'))
			const curSizeDom = sizeOptionDom.querySelector(`[data-size='${payload.size}']`)
			if (curSizeDom) {
				sizeSelectDom.innerText = curSizeDom.innerText
				curSizeDom.classList.add('active')
			} else {
				sizeSelectDom.innerText = `${payload.size}`
			}
			payload.bold ? boldDom.classList.add('active') : boldDom.classList.remove('active')
			payload.italic ? italicDom.classList.add('active') : italicDom.classList.remove('active')
			payload.underline ? underlineDom.classList.add('active') : underlineDom.classList.remove('active')
			payload.strikeout ? strikeoutDom.classList.add('active') : strikeoutDom.classList.remove('active')

			// 行布局
			leftDom.classList.remove('active')
			centerDom.classList.remove('active')
			rightDom.classList.remove('active')
			alignmentDom.classList.remove('active')
			if (payload.rowFlex && payload.rowFlex === 'right') {
				rightDom.classList.add('active')
			} else if (payload.rowFlex && payload.rowFlex === 'center') {
				centerDom.classList.add('active')
			} else if (payload.rowFlex && payload.rowFlex === 'alignment') {
				alignmentDom.classList.add('active')
			} else {
				leftDom.classList.add('active')
			}

			// 行间距
			rowOptionDom.querySelectorAll('li').forEach((li) => li.classList.remove('active'))
			const curRowMarginDom = rowOptionDom.querySelector(`[data-rowmargin='${payload.rowMargin}']`)
			curRowMarginDom.classList.add('active')

			// 功能
			payload.undo ? undoDom.classList.remove('no-allow') : undoDom.classList.add('no-allow')
			payload.redo ? redoDom.classList.remove('no-allow') : redoDom.classList.add('no-allow')
			payload.painter ? painterDom.classList.add('active') : painterDom.classList.remove('active')

			// 标题
			titleOptionDom.querySelectorAll('li').forEach((li) => li.classList.remove('active'))
			if (payload.level) {
				const curTitleDom = titleOptionDom.querySelector(`[data-level='${payload.level}']`)
				titleSelectDom.innerText = curTitleDom.innerText
				curTitleDom.classList.add('active')
			} else {
				titleSelectDom.innerText = '正文'
				titleOptionDom.querySelector('li:first-child').classList.add('active')
			}
		})

		//监听保存
		instance.value.eventBus.on('saved', (payload) => {
			let docId = formData.value.id
			const htmlJson = instance.value.command.getHTML()
			formData.value.header = htmlJson.header
			formData.value.main = htmlJson.main
			formData.value.footer = htmlJson.footer

			if (docId) {
				docModalVisible.value = false
				formData.value.docId = docId
				appDocItemApi
					.appDocItemSubmitForm(formData.value, formData.value.id)
					.then(() => {
						onClose()
						emit('successful')
					})
					.finally(() => {
						docModalVisible.value = false
						window.location.reload()
						// submitLoading.value = false
					})
			} else {
				docModalVisible.value = true
			}
		})
	})

	const handleOk = () => {
		// console.log(formData.value)
		appDocItemApi
			.appDocItemSubmitForm(formData.value, formData.value.id)
			.then(() => {
				onClose()
				emit('successful')
			})
			.finally(() => {
				docModalVisible.value = false
				window.location.reload()
			})
	}

	// 字体选择
	const fontClick = () => {
		const options = document.querySelector('.menu-item__font .options')
		options.classList.toggle('visible')
	}
	// 字体选择
	const fontChange = (e) => {
		instance.value.command.executeFont(e.target.dataset.family)
	}
	// 字体大小选择
	const sizeClick = () => {
		const options = document.querySelector('.menu-item__size .options')
		options.classList.toggle('visible')
	}
	// 字体大小选择
	const sizeChange = (e) => {
		instance.value.command.executeSize(Number(e.target.dataset.size))
	}

	// 文字增大
	const sizeAddClick = (e) => {
		instance.value.command.executeSizeAdd()
	}
	// 文字减小
	const sizeMinusClick = (e) => {
		instance.value.command.executeSizeMinus()
	}

	// 文字减小
	const executeBold = (e) => {
		instance.value.command.executeBold()
	}

	// 文字斜体
	const executeItalic = (e) => {
		instance.value.command.executeItalic()
	}

	// 文字下划线
	const executeStrikeout = (e) => {
		instance.value.command.executeStrikeout()
	}

	// 上标
	const executeSuperscript = (e) => {
		instance.value.command.executeSuperscript()
	}

	//下标
	const executeSubscript = (e) => {
		instance.value.command.executeSubscript()
	}

	// 选择颜色

	const colorClick = (e) => {
		const colorControlDom = document.querySelector('#color')
		colorControlDom.click()
		colorControlDom.addEventListener('input', (e) => {
			instance.value.command.executeColor(colorControlDom.value)
		})
	}

	//高亮
	const highlightClick = (e) => {
		const colorControlDom = document.querySelector('#highlight')
		colorControlDom.click()
		colorControlDom.addEventListener('input', (e) => {
			instance.value.command.executeHighlight(colorControlDom.value)
		})
	}

	//居左对齐
	const executeLeft = (e) => {
		instance.value.command.executeRowFlex(RowFlex.LEFT)
	}

	//居中对齐
	const executeCenter = (e) => {
		instance.value.command.executeRowFlex(RowFlex.CENTER)
	}

	//居右对齐
	const executeRight = (e) => {
		instance.value.command.executeRowFlex(RowFlex.RIGHT)
	}

	//两端对齐
	const executeAlignment = (e) => {
		instance.value.command.executeRowFlex(RowFlex.ALIGNMENT)
	}

	//underline
	const underlineClick = () => {
		const options = document.querySelector('.menu-item__underline .options')
		options.classList.toggle('visible')
	}
	//underline
	const underlineChange = (e) => {
		instance.value.command.executeUnderline({
			style: e
		})
	}
	//标题
	const titleClick = () => {
		const options = document.querySelector('.menu-item__title .options')
		options.classList.toggle('visible')
	}
	//标题
	const titleChange = (e) => {
		instance.value.command.executeTitle(e.target.dataset.level || null)
	}

	//行间距
	const rowMarginClick = () => {
		const options = document.querySelector('.menu-item__row-margin .options')
		options.classList.toggle('visible')
	}
	//行间距
	const rowMarginChange = (e) => {
		instance.value.command.executeRowMargin(Number(e.target.dataset.rowmargin))
	}
	//列表
	const listClick = () => {
		const options = document.querySelector('.menu-item__list .options')
		options.classList.toggle('visible')
	}
	//列表
	const listChange = (e) => {
		const { listType, listStyle } = e.target.dataset
		instance.value.command.executeList(listType, listStyle)
	}
	//表格

	const tableClick = () => {
		const tablePanelContainer = document.querySelector('.menu-item__table__collapse')
		tablePanelContainer.style.display = 'block'
		const tablePanel = document.querySelector('.table-panel')
		for (let i = 0; i < 10; i++) {
			const tr = document.createElement('tr')
			tr.classList.add('table-row')
			const trCellList = []
			for (let j = 0; j < 10; j++) {
				const td = document.createElement('td')
				td.classList.add('table-cel')
				tr.append(td)
				trCellList.push(td)
			}
			tablePanel.append(tr)
			tableCellList.value.push(trCellList)
		}
	}
	//表格关闭
	const recoveryTable = () => {
		// 还原选择样式、标题、选择行列
		removeAllTableCellSelect()
		setTableTitle('插入')
		colIndex.value = 0
		rowIndex.value = 0
		tableCellList.value = []
		// 隐藏panel
		const tablePanelContainer = document.querySelector('.menu-item__table__collapse')
		const tablePanel = document.querySelector('.table-panel')
		tablePanel.innerHTML = ''
		tablePanelContainer.style.display = 'none'
	}
	//表格选择节点
	const tableMouseMove = (e) => {
		const celSize = 16
		const rowMarginTop = 10
		const celMarginRight = 6
		const { offsetX, offsetY } = e
		// 移除所有选择
		removeAllTableCellSelect()
		colIndex.value = Math.ceil(offsetX / (celSize + celMarginRight)) || 1
		rowIndex.value = Math.ceil(offsetY / (celSize + rowMarginTop)) || 1
		// 改变选择样式
		tableCellList.value.forEach((tr, trIndex) => {
			tr.forEach((td, tdIndex) => {
				if (tdIndex < colIndex.value && trIndex < rowIndex.value) {
					td.classList.add('active')
				}
			})
		})
		// 改变表格标题
		setTableTitle(`${rowIndex.value}×${colIndex.value}`)
	}
	//设置表格标题
	const setTableTitle = (title) => {
		const tableTitle = document.querySelector('.table-select')
		tableTitle.innerText = title
	}
	//移除所有选择
	const removeAllTableCellSelect = () => {
		tableCellList.value.forEach((tr) => {
			tr.forEach((td) => {
				td.classList.remove('active')
			})
		})
	}
	//插入表格
	const tableRowCellClick = () => {
		instance.value.command.executeInsertTable(rowIndex.value, colIndex.value)
		recoveryTable()
	}
	//分割线
	const separatorClick = () => {
		const options = document.querySelector('.menu-item__separator .options')
		options.classList.toggle('visible')
	}
	//分割线
	const separatorChange = (e) => {
		const separatorList = e?.split(',').map((item) => Number(item))
		instance.value.command.executeSeparator(separatorList)
	}
	//图片
	const imageClick = () => {
		const imageFileDom = document.querySelector('#image')
		imageFileDom.click()
		imageFileDom.addEventListener('change', (e) => {
			const file = e.target.files[0]
			const reader = new FileReader()
			reader.readAsDataURL(file)
			reader.onload = (e) => {
				const image = new Image()
				image.src = e.target.result
				image.onload = function () {
					instance.value.command.executeImage({
						value: e.target.result,
						width: image.width,
						height: image.height
					})
					imageFileDom.value = ''
				}
			}
		})
	}
	//超链接
	const hyperlinkClick = () => {
		hyperlinkFormRef.value.validate().then(() => {
			instance.value.command.executeHyperlink({
				type: ElementType.HYPERLINK,
				value: '',
				url: hyperlink.value.hyperlinkText,
				valueList: splitText(hyperlink.value.hyperlinkUrl).map((n) => ({
					value: n,
					size: 16
				}))
			})
			hyperlinkModalVisible.value = false
			hyperlinkFormRef.value.resetFields()
			hyperlink.value = {}
		})
	}

	//水印
	const watermarkClick = () => {
		const options = document.querySelector('.menu-item__watermark .options')
		options.classList.toggle('visible')
	}

	//水印确认
	const watermarkConfirm = () => {
		watermarkFormRef.value.validate().then(() => {
			instance.value.command.executeAddWatermark({
				data: watermark.value.content,
				color: watermark.value.color,
				size: Number(watermark.value.fontSize)
			})

			watermarkModalVisible.value = false
			watermarkFormRef.value.resetFields()
			watermark.value = {}
		})
	}

	//代码块确认
	// #region 已有插件
	function getPrismKindStyle(payload) {
		switch (payload) {
			case 'comment':
			case 'prolog':
			case 'doctype':
			case 'cdata':
				return { color: '#008000', italic: true }
			case 'namespace':
				return { opacity: 0.7 }
			case 'string':
				return { color: '#A31515' }
			case 'punctuation':
			case 'operator':
				return { color: '#393A34' }
			case 'url':
			case 'symbol':
			case 'number':
			case 'boolean':
			case 'variable':
			case 'constant':
			case 'inserted':
				return { color: '#36acaa' }
			case 'atrule':
			case 'keyword':
			case 'attr-value':
				return { color: '#0000ff' }
			case 'function':
				return { color: '#b9a40a' }
			case 'deleted':
			case 'tag':
				return { color: '#9a050f' }
			case 'selector':
				return { color: '#00009f' }
			case 'important':
				return { color: '#e90', bold: true }
			case 'italic':
				return { italic: true }
			case 'class-name':
			case 'property':
				return { color: '#2B91AF' }
			case 'attr-name':
			case 'regex':
			case 'entity':
				return { color: '#ff0000' }
			default:
				return null
		}
	}
	function formatPrismToken(payload) {
		var formatTokenList = []
		function format(tokenList) {
			for (var i = 0; i < tokenList.length; i++) {
				var element = tokenList[i]
				if (typeof element === 'string') {
					formatTokenList.push({
						content: element
					})
				} else if (Array.isArray(element.content)) {
					format(element.content)
				} else {
					var type = element.type,
						content = element.content
					if (typeof content === 'string') {
						formatTokenList.push(
							Object.assign(
								{
									type: type,
									content: content
								},
								getPrismKindStyle(type)
							)
						)
					}
				}
			}
		}
		format(payload)
		return formatTokenList
	}
	// #endregion
	const codeBoxConfirm = () => {
		codeBoxFormRef.value.validate().then(() => {
			// #region 已有插件
			// const tokenList = prism.tokenize(codeBox.value.content, prism.languages.javascript)
			// const formatTokenList = formatPrismToken(tokenList)
			// const elementList = []
			// for (let i = 0; i < formatTokenList.length; i++) {
			// 	const formatToken = formatTokenList[i]
			// 	const tokenStringList = splitText(formatToken.content)
			// 	for (let j = 0; j < tokenStringList.length; j++) {
			// 		const value = tokenStringList[j]
			// 		const element = {
			// 			value
			// 		}
			// 		if (formatToken.color) {
			// 			element.color = formatToken.color
			// 		}
			// 		if (formatToken.bold) {
			// 			element.bold = true
			// 		}
			// 		if (formatToken.italic) {
			// 			element.italic = true
			// 		}
			// 		elementList.push(element)
			// 	}
			// }
			// elementList.unshift({
			// 	value: '\n'
			// })
			// instance.value.command.executeInsertElementList(elementList)
			// #endregion
			instance.value.command.executeInsertCodeblock(codeBox.value.content)
			codeBoxVisible.value = false
			codeBoxFormRef.value.resetFields()
			codeBox.value = {}
		})
	}

	//LateX
	const latexBoxConfirm = () => {
		latexBoxFormRef.value.validate().then(() => {
			instance.value.command.executeInsertElementList([
				{
					type: ElementType.LATEX,
					value: latexBox.value.content
				}
			])
			latexVisible.value = false
			latexBoxFormRef.value.resetFields()
			latexBox.value = {}
		})
	}
	//日期
	const dateClick = () => {
		const dateDomOptionDom = document.querySelector('.menu-item__date .options')
		dateDomOptionDom.classList.toggle('visible')

		// 定位调整
		const bodyRect = document.body.getBoundingClientRect()
		const dateDomOptionRect = dateDomOptionDom.getBoundingClientRect()
		if (dateDomOptionRect.left + dateDomOptionRect.width > bodyRect.width) {
			dateDomOptionDom.style.right = '0px'
			dateDomOptionDom.style.left = 'unset'
		} else {
			dateDomOptionDom.style.right = 'unset'
			dateDomOptionDom.style.left = '0px'
		}
		// 当前日期
		const date = new Date()
		const year = date.getFullYear().toString()
		const month = (date.getMonth() + 1).toString().padStart(2, '0')
		const day = date.getDate().toString().padStart(2, '0')
		const hour = date.getHours().toString().padStart(2, '0')
		const minute = date.getMinutes().toString().padStart(2, '0')
		const second = date.getSeconds().toString().padStart(2, '0')
		const dateString = `${year}-${month}-${day}`
		const dateTimeString = `${dateString} ${hour}:${minute}:${second}`
		dateDomOptionDom.querySelector('li:first-child').innerText = dateString
		dateDomOptionDom.querySelector('li:last-child').innerText = dateTimeString
	}

	//日期选择
	const dateChange = (e) => {
		instance.value.command.executeInsertElementList([
			{
				type: ElementType.DATE,
				value: '',
				dateFormat: e.target.dataset.format,
				valueList: [
					{
						value: e.target.innerText.trim()
					}
				]
			}
		])
	}
	//搜索

	const searchClick = () => {
		const searchCollapseDom = document.querySelector('.menu-item__search__collapse')
		const searchResultDom = searchCollapseDom.querySelector('.search-result')
		const searchInputDom = document.querySelector('.menu-item__search__collapse__search input')
		const replaceInputDom = document.querySelector('.menu-item__search__collapse__replace input')
		const searchDom = document.querySelector('.menu-item__search')
		function setSearchResult() {
			const result = instance.value.command.getSearchNavigateInfo()
			if (result) {
				const { index, count } = result
				searchResultDom.innerText = `${index}/${count}`
			} else {
				searchResultDom.innerText = ''
			}
		}

		searchCollapseDom.style.display = 'block'
		const bodyRect = document.body.getBoundingClientRect()
		const searchRect = searchDom.getBoundingClientRect()
		const searchCollapseRect = searchCollapseDom.getBoundingClientRect()
		if (searchRect.left + searchCollapseRect.width > bodyRect.width) {
			searchCollapseDom.style.right = '0px'
			searchCollapseDom.style.left = 'unset'
		} else {
			searchCollapseDom.style.right = 'unset'
		}
		searchInputDom.focus()

		searchCollapseDom.querySelector('span').onclick = function () {
			searchCollapseDom.style.display = 'none'
			searchInputDom.value = ''
			replaceInputDom.value = ''
			instance.value.command.executeSearch(null)
			setSearchResult()
		}
		searchInputDom.oninput = function () {
			instance.value.command.executeSearch(searchInputDom.value || null)
			setSearchResult()
		}
		searchInputDom.onkeydown = function (evt) {
			if (evt.key === 'Enter') {
				instance.value.command.executeSearch(searchInputDom.value || null)
				setSearchResult()
			}
		}
		searchCollapseDom.querySelector('button').onclick = function () {
			const searchValue = searchInputDom.value
			const replaceValue = replaceInputDom.value
			if (searchValue && replaceValue && searchValue !== replaceValue) {
				instance.value.command.executeReplace(replaceValue)
			}
		}
		searchCollapseDom.querySelector('.arrow-left').onclick = function () {
			instance.value.command.executeSearchNavigatePre()
			setSearchResult()
		}
		searchCollapseDom.querySelector('.arrow-right').onclick = function () {
			instance.value.command.executeSearchNavigateNext()
			setSearchResult()
		}
	}

	//控件
	const controlClick = () => {
		const controlCollapseDom = document.querySelector('.menu-item__control .options')
		controlCollapseDom.classList.toggle('visible')
	}

	//控件确认
	const controlboxConfirm = () => {
		controlboxFormRef.value.validate().then(() => {
			if (controlbox.value.type == ControlType.TEXT) {
				instance.value.command.executeInsertElementList([
					{
						type: ElementType.CONTROL,
						value: '',
						control: {
							type: controlbox.value.type,
							value: controlbox.value.default
								? [
										{
											value: controlbox.value.default
										}
								  ]
								: null,
							placeholder: controlbox.value.placeholder
						}
					}
				])
			} else if (controlbox.value.type == ControlType.SELECT) {
				instance.value.command.executeInsertElementList([
					{
						type: ElementType.CONTROL,
						value: '',
						control: {
							type: controlbox.value.type,
							placeholder: controlbox.value.placeholder,
							code: controlbox.value.default,
							value: null,
							valueSets: JSON.parse(controlbox.value.list)
						}
					}
				])
			} else if (controlbox.value.type == ControlType.CHECKBOX) {
				instance.command.executeInsertElementList([
					{
						type: ElementType.CONTROL,
						value: '',
						control: {
							type: controlbox.value.type,
							placeholder: controlbox.value.placeholder,
							code: controlbox.value.default,
							value: null,
							valueSets: JSON.parse(controlbox.value.list)
						}
					}
				])
			}
			controlModalVisible.value = false
			controlboxFormRef.value.resetFields()
			controlbox.value = {}
		})
	}

	//内容块
	const contentBlockConfirm = () => {
		contentBlockFormRef.value.validate().then(() => {
			const block = {
				type: contentBlock.value.type
			}
			if (block.type === BlockType.IFRAME) {
				if (!contentBlock.value.url && !contentBlock.value.html) return
				block.iframeBlock = {
					src: contentBlock.value.url,
					srcdoc: contentBlock.value.html
				}
			} else if (block.type === BlockType.VIDEO) {
				if (!contentBlock.value.url) return
				block.videoBlock = {
					src: contentBlock.value.url
				}
			}
			console.log(block)
			const blockElement = {
				type: ElementType.BLOCK,
				value: '',
				height: Number(contentBlock.value.height),
				block,
				width: Number(contentBlock.value.width)
			}
			instance.value.command.executeInsertElementList([blockElement])
			contentBlockModalVisible.value = false
			contentBlockFormRef.value.resetFields()
			contentBlock.value = {}
		})
	}

	//目录
	async function updateCatalog() {
		const catalog = await instance.value.command.getCatalog()
		const catalogMainDom = document.querySelector('.catalog__main')
		catalogMainDom.innerHTML = ''
		if (catalog) {
			const appendCatalog = (parent, catalogItems) => {
				for (let c = 0; c < catalogItems.length; c++) {
					const catalogItem = catalogItems[c]
					const catalogItemDom = document.createElement('div')
					catalogItemDom.classList.add('catalog-item')
					// 渲染
					const catalogItemContentDom = document.createElement('div')
					catalogItemContentDom.classList.add('catalog-item__content')
					const catalogItemContentSpanDom = document.createElement('span')
					catalogItemContentSpanDom.innerText = catalogItem.name
					catalogItemContentDom.append(catalogItemContentSpanDom)
					// 定位
					catalogItemContentDom.onclick = () => {
						instance.value.command.executeLocationCatalog(catalogItem.id)
					}
					catalogItemDom.append(catalogItemContentDom)
					if (catalogItem.subCatalog && catalogItem.subCatalog.length) {
						appendCatalog(catalogItemDom, catalogItem.subCatalog)
					}
					// 追加
					parent.append(catalogItemDom)
				}
			}
			appendCatalog(catalogMainDom, catalog)
		}
	}
	const catelogClick = () => {
		switchCatalog()
	}
	const catalogClose = () => {
		switchCatalog()
	}

	const switchCatalog = () => {
		const catalogModeDom = document.querySelector('.catalog-mode')
		const catalogDom = document.querySelector('.catalog')
		const catalogHeaderCloseDom = document.querySelector('.catalog__header__close')
		isCatalogShow = !isCatalogShow
		if (isCatalogShow) {
			catalogDom.style.display = 'block'
			updateCatalog()
		} else {
			catalogDom.style.display = 'none'
		}
	}
	const handleContentChange = async function () {
		// 字数
		const wordCount = await instance.value.command.getWordCount()
		document.querySelector('.word-count').innerText = `${wordCount || 0}`
		// 目录
		if (isCatalogShow) {
			nextTick(() => {
				updateCatalog()
			})
		}
	}

	//分页切换
	const pageModeClick = () => {
		const pageModeDom = document.querySelector('.page-mode .options')
		pageModeDom.classList.toggle('visible')
	}
	//分页确认
	const pageModeChange = (e) => {
		instance.value.command.executePageMode(e.target.dataset.pageMode)
	}

	// 7. 编辑器使用模式
	let modeIndex = 0
	const editorModeClick = () => {
		const modeList = [
			{
				mode: EditorMode.EDIT,
				name: '编辑模式'
			},
			{
				mode: EditorMode.CLEAN,
				name: '清洁模式'
			},
			{
				mode: EditorMode.READONLY,
				name: '只读模式'
			},
			{
				mode: EditorMode.FORM,
				name: '表单模式'
			},
			{
				mode: EditorMode.PRINT,
				name: '打印模式'
			}
		]
		const modeElement = document.querySelector('.editor-mode')
		// 模式选择循环
		modeIndex === modeList.length - 1 ? (modeIndex = 0) : modeIndex++
		// 设置模式
		const { name, mode } = modeList[modeIndex]
		modeElement.innerText = name
		instance.value.command.executeMode(mode)
		// 设置菜单栏权限视觉反馈
		const isReadonly = mode === EditorMode.READONLY
		const enableMenuList = ['search', 'print']
		document.querySelectorAll('.menu-item>div').forEach((dom) => {
			const menu = dom.dataset.menu
			isReadonly && (!menu || !enableMenuList.includes(menu))
				? dom.classList.add('disable')
				: dom.classList.remove('disable')
		})
	}

	//纸张类型
	const paperTypeClick = () => {
		const paperTypeDom = document.querySelector('.paper-size .options')
		paperTypeDom.classList.toggle('visible')
	}
	//纸张类型确认
	const paperTypeChange = (e) => {
		const paperTypeDom = document.querySelector('.paper-size .options')
		let [width, height] = e.target.dataset.paperSize.split('*').map((item) => Number(item))
		instance.value.command.executePaperSize(width, height)

		// 纸张状态回显
		paperTypeDom.querySelectorAll('li').forEach((child) => child.classList.remove('active'))
		e.target.classList.add('active')
	}
	//纸张方向
	const paperDirectionClick = () => {
		const paperDirectionDom = document.querySelector('.paper-direction .options')
		paperDirectionDom.classList.toggle('visible')
	}
	//纸张方向确认
	const paperDirectionChange = (e) => {
		const paperDirectionDom = document.querySelector('.paper-direction .options')
		instance.value.command.executePaperDirection(e.target.dataset.paperDirection)
		// 纸张方向状态回显
		paperDirectionDom.querySelectorAll('li').forEach((child) => child.classList.remove('active'))
		e.target.classList.add('active')
	}

	//页边距
	const pageMarginClick = () => {
		pageMarginVisible.value = true
		const [top, right, bottom, left] = instance.value.command.getPaperMargin()
		pageMargin.value = { top, right, bottom, left }
	}
	//页边距确认
	const pageMarginConfirm = () => {
		pageMarginFormRef.value.validate().then(() => {
			const { top, right, bottom, left } = pageMargin.value
			instance.value.command.executeSetPaperMargin([top, right, bottom, left])
			pageMarginVisible.value = false
		})
	}

	//全屏

	const fullScreenClick = () => {
		const fullscreenDom = document.querySelector('.fullscreen')
		document.addEventListener('fullscreenchange', () => {
			fullscreenDom.classList.toggle('exist')
		})
		toggleFullscreen()
	}
	function toggleFullscreen() {
		if (!document.fullscreenElement) {
			isFullScreen.value = true
			document.documentElement.requestFullscreen()
		} else {
			document.exitFullscreen()
			isFullScreen.value = false
		}
	}
	window.addEventListener('keydown', (evt) => {
		if (evt.key === 'F11') {
			toggleFullscreen()
			evt.preventDefault()
		}
	})

	//编辑器配置
	const editorOptionClick = () => {
		editorOptionVisible.value = true
		const options = instance.value.command.getOptions()
		editorOption.value.content = JSON.stringify(options, null, 2)
	}

	//编辑器配置确认
	const editorOptionConfirm = () => {
		editorOptionFormRef.value.validate().then(() => {
			const options = instance.value.command.getOptions()
			const newOption = JSON.parse(editorOption.value.content)
			Object.keys(newOption).forEach((key) => {
				Reflect.set(options, key, newOption[key])
			})
			instance.value.command.executeForceUpdate()
			editorOptionVisible.value = false
			editorOptionFormRef.value.resetFields()
			editorOption.value = {}
		})
	}
</script>

<style lang="less" scoped>
	@import url(./style.less);
</style>

```


```css
ul {
	list-style: none;
}
.menu {
	width: 100%;
	height: 60px;
	top: 0;
	z-index: 9;
	position: fixed;
	display: flex;
	align-items: center;
	justify-content: center;
	background: #f2f4f7;
	box-shadow: 0 2px 4px 0 transparent;
	.menu-divider {
		width: 1px;
		height: 16px;
		margin: 0 8px;
		display: inline-block;
		background-color: #cfd2d8;
	}
	.menu-item {
		height: 24px;
		display: flex;
		align-items: center;
		position: relative;
	}
	.menu-item > div {
		width: 24px;
		height: 24px;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		margin: 0 2px;
	}
	.menu-item > div:hover {
		background: rgba(25, 55, 88, 0.04);
	}
	.menu-item > div > span {
		width: 16px;
		height: 3px;
		display: inline-block;
		border: 1px solid #e2e6ed;
	}

	.menu-item .select {
		border: none;
		font-size: 12px;
		line-height: 24px;
	}

	.menu-item .select::after {
		position: absolute;
		content: '';
		top: 11px;
		width: 0;
		height: 0;
		right: 2px;
		border-color: #767c85 transparent transparent;
		border-style: solid solid none;
		border-width: 3px 3px 0;
	}

	.menu-item .options {
		width: 70px;
		position: absolute;
		left: 0;
		top: 25px;
		padding: 10px;
		background: #fff;
		font-size: 14px;
		box-shadow: 0 2px 12px 0 rgb(56 56 56 / 20%);
		border: 1px solid #e2e6ed;
		border-radius: 2px;
		display: none;
		box-sizing: content-box;
	}

	.menu-item .options.visible {
		display: block;
	}

	.menu-item .options li {
		padding: 5px;
		margin: 5px 0;
		user-select: none;
		transition: all 0.3s;
	}

	.menu-item .options li:hover {
		background-color: #ebecef;
	}

	.menu-item .options li.active {
		background-color: #e2e6ed;
	}

	.menu-item .menu-item__font {
		width: 65px;
		position: relative;
	}

	.menu-item .menu-item__size {
		width: 50px;
		text-align: center;
		position: relative;
	}

	.menu-item__font .select,
	.menu-item__size .select {
		width: 100%;
		height: 100%;
	}
	.menu-item .menu-item__underline {
		width: 30px;
		position: relative;
	}
	.menu-item__underline .select {
		width: 100%;
		height: 100%;
	}

	.menu-item .menu-item__underline .options {
		width: 128px;
	}

	.menu-item .menu-item__underline li {
		padding: 1px 0px;
	}

	.menu-item__underline li i {
		pointer-events: none;
	}

	.menu-item__color,
	.menu-item__highlight {
		display: flex;
		flex-direction: column;
	}

	.menu-item__color #color,
	.menu-item__highlight #highlight {
		width: 1px;
		height: 1px;
		visibility: hidden;
		outline: none;
		appearance: none;
	}

	.menu-item__color span {
		background-color: #000000;
	}

	.menu-item__highlight span {
		background-color: #ffff00;
	}

	.menu-item .menu-item__title {
		width: 60px;
		position: relative;
	}

	.menu-item__title .select {
		width: calc(100% - 20px);
		height: 100%;
	}

	.menu-item__title .options {
		width: 80px;
	}
	.menu-item__row-margin {
		position: relative;
	}

	.menu-item__list {
		position: relative;
	}

	.menu-item__list .options {
		width: 110px;
	}

	.menu-item__list .options > ul > li * {
		pointer-events: none;
	}

	.menu-item__list .options > ul > li li {
		margin-left: 18px;
	}

	.menu-item__list .options > ul > li[data-list-style='checkbox'] li::marker {
		font-size: 11px;
	}

	.menu-item__image input {
		display: none;
	}

	.menu-item__table {
		position: relative;
	}

	.menu-item .menu-item__table__collapse {
		width: 270px;
		height: 310px;
		background: #fff;
		box-shadow: 0 2px 12px 0 rgb(56 56 56 / 20%);
		border: 1px solid #e2e6ed;
		box-sizing: border-box;
		border-radius: 2px;
		position: absolute;
		display: none;
		z-index: 99;
		top: 25px;
		left: 0;
		padding: 14px 27px;
		cursor: auto;

		.table-close {
			position: absolute;
			right: 10px;
			top: 5px;
			cursor: pointer;
		}

		.table-title span {
			font-size: 12px;
			color: #3d4757;
			display: inline;
			margin: 0;
		}

		:deep(.table-panel) {
			cursor: pointer;
			.table-row {
				display: flex;
				flex-wrap: nowrap;
				margin-top: 10px;
				pointer-events: none;
				.table-cel {
					width: 16px;
					height: 16px;
					box-sizing: border-box;
					border: 1px solid #e2e6ed;
					background: #fff;
					position: relative;
					margin-right: 6px;
					pointer-events: none;
				}
				.table-cel.active {
					border: 1px solid rgba(73, 145, 242, 0.2);
					background: rgba(73, 145, 242, 0.15);
				}
				.table-cel:last-child {
					margin-right: 0;
				}
			}
		}
	}

	.menu-item .menu-item__table__collapse .table-close:hover {
		color: #7d7e80;
	}

	.menu-item .menu-item__table__collapse:hover {
		background: #fff;
	}

	.menu-item .menu-item__table__collapse .table-title {
		display: flex;
		justify-content: flex-start;
		padding-bottom: 5px;
		border-bottom: 1px solid #e2e6ed;
	}

	.menu-item__separator {
		position: relative;
	}

	.menu-item .menu-item__separator .options {
		width: 128px;
	}

	.menu-item .menu-item__separator li {
		padding: 1px 5px;
	}

	.menu-item__separator li i {
		pointer-events: none;
	}

	.menu-item__watermark {
		position: relative;
	}

	.menu-item__control {
		position: relative;
	}

	.menu-item__date {
		position: relative;
	}

	.menu-item__date .options {
		width: 160px;
	}

	.menu-item .menu-item__control .options {
		width: 55px;
	}

	.menu-item__search {
		position: relative;
	}

	.menu-item .menu-item__search__collapse {
		width: 260px;
		height: 72px;
		box-sizing: border-box;
		position: absolute;
		display: none;
		z-index: 99;
		top: 25px;
		left: 0;
		background: #ffffff;
		box-shadow: 0px 5px 5px #e3dfdf;
	}

	.menu-item .menu-item__search__collapse:hover {
		background: #ffffff;
	}

	.menu-item .menu-item__search__collapse > div {
		width: 250px;
		height: 36px;
		padding: 0 5px;
		line-height: 36px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		border-radius: 4px;
	}

	.menu-item .menu-item__search__collapse > div input {
		width: 205px;
		height: 27px;
		appearance: none;
		background-color: #fff;
		background-image: none;
		border-radius: 4px;
		border: 1px solid #ebebeb;
		box-sizing: border-box;
		color: #606266;
		display: inline-block;
		line-height: 27px;
		outline: none;
		padding: 0 5px;
	}

	.menu-item .menu-item__search__collapse > div span {
		height: 100%;
		color: #dcdfe6;
		font-size: 25px;
		display: inline-block;
		border: 0;
		padding: 0 10px;
	}

	.menu-item .menu-item__search__collapse__replace button {
		display: inline-block;
		border: 1px solid #e2e6ed;
		border-radius: 2px;
		background: #fff;
		line-height: 22px;
		padding: 0 6px;
		white-space: nowrap;
		margin-left: 4px;
		cursor: pointer;
		font-size: 12px;
	}

	.menu-item .menu-item__search__collapse__replace button:hover {
		background: rgba(25, 55, 88, 0.04);
	}

	.menu-item .menu-item__search__collapse__search {
		position: relative;
	}

	.menu-item .menu-item__search__collapse__search label {
		right: 110px;
		font-size: 12px;
		color: #3d4757;
		position: absolute;
	}

	.menu-item .menu-item__search__collapse__search > input {
		padding: 5px 90px 5px 5px !important;
	}

	.menu-item .menu-item__search__collapse__search > div {
		width: 28px;
		height: 27px;
		display: flex;
		justify-content: center;
		align-items: center;
		position: absolute;
		border-left: 1px solid #e2e6ed;
		transition: all 0.5s;
	}

	.menu-item .menu-item__search__collapse__search > div:hover {
		background-color: rgba(25, 55, 88, 0.04);
	}

	.menu-item .menu-item__search__collapse__search i {
		width: 6px;
		height: 8px;
		transform: translateY(1px);
	}

	.menu-item .menu-item__search__collapse__search .arrow-left {
		right: 76px;
	}

	.menu-item .menu-item__search__collapse__search .arrow-right {
		right: 48px;
	}
}

.catalog {
	width: 250px;
	position: fixed;
	left: 0;
	bottom: 0;
	top: 100px;
	padding: 0 20px 40px 20px;
}

.catalog .catalog__header {
	height: 48px;
	display: flex;
	align-items: center;
	justify-content: space-between;
	border-bottom: 1px solid #e2e6ed;
}

.catalog .catalog__header span {
	color: #3d4757;
	font-size: 14px;
	font-weight: bold;
}

.catalog .catalog__header > div:hover {
	background: rgba(235, 238, 241);
}

.catalog__main {
	height: calc(100% - 60px);
	padding: 10px 0;
	overflow-y: auto;
	overflow-x: hidden;
}

.catalog__main .catalog-item {
	width: 100%;
	padding-left: 10px;
	box-sizing: border-box;
}

.catalog__main > .catalog-item {
	padding-left: 0;
}

.catalog__main .catalog-item .catalog-item__content {
	width: 100%;
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}

.catalog__main .catalog-item .catalog-item__content:hover > span {
	color: #4991f2;
}

.catalog__main .catalog-item .catalog-item__content span {
	color: #3d4757;
	line-height: 30px;
	font-size: 12px;
	white-space: nowrap;
	cursor: pointer;
	user-select: none;
}

.editor > div {
	margin: 80px auto;
}

.ce-page-container canvas {
	box-shadow: rgb(158 161 165 / 40%) 0px 2px 12px 0px;
}

.comment {
	width: 250px;
	height: 650px;
	position: fixed;
	transform: translateX(420px);
	top: 200px;
	left: 50%;
	overflow-y: auto;
}

.comment-item {
	background: #ffffff;
	border: 1px solid #e2e6ed;
	position: relative;
	border-radius: 8px;
	padding: 15px;
	font-size: 14px;
	margin-bottom: 20px;
	cursor: pointer;
	transition: all 0.5s;
}

.comment-item:hover {
	border-color: #c0c6cf;
	box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.comment-item.active {
	border-color: #e99d00;
	box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}

.comment-item__title {
	height: 22px;
	position: relative;
	display: flex;
	align-items: center;
	color: #c1c6ce;
}

.comment-item__title span:first-child {
	background-color: #dbdbdb;
	width: 4px;
	height: 16px;
	margin-right: 5px;
	display: inline-block;
	border-radius: 999px;
}

.comment-item__title span:nth-child(2) {
	width: 200px;
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}

.comment-item__title i:hover {
	opacity: 0.6;
}

.comment-item__info {
	height: 28px;
	display: flex;
	align-items: center;
	justify-content: space-between;
}

.comment-item__info > span:first-child {
	font-weight: 600;
}

.comment-item__info > span:last-child {
	color: #c1c6ce;
}

.comment-item__content {
	line-height: 22px;
}

.footer {
	width: 100%;
	height: 30px;
	display: flex;
	align-items: center;
	justify-content: space-between;
	background: #f2f4f7;
	z-index: 9;
	position: fixed;
	bottom: 0;
	left: 0;
	font-size: 12px;
	padding: 0 4px 0 20px;
	box-sizing: border-box;
}

.footer > div:first-child {
	display: flex;
	align-items: center;
}

.footer .catalog-mode {
	padding: 1px;
	position: relative;
}

.footer .page-mode {
	padding: 1px;
	position: relative;
}

.footer .options {
	width: 70px;
	position: absolute;
	left: 0;
	bottom: 25px;
	padding: 10px;
	background: #fff;
	font-size: 14px;
	box-shadow: 0 2px 12px 0 rgb(56 56 56 / 20%);
	border: 1px solid #e2e6ed;
	border-radius: 2px;
	display: none;
}

.footer .options.visible {
	display: block;
}

.footer .options li {
	padding: 5px;
	margin: 5px 0;
	user-select: none;
	transition: all 0.3s;
	text-align: center;
	cursor: pointer;
}

.footer .options li:hover {
	background-color: #ebecef;
}

.footer .options li.active {
	background-color: #e2e6ed;
}

.footer > div:first-child > span {
	display: inline-block;
	margin-right: 5px;
	letter-spacing: 1px;
}

.footer > div:last-child {
	display: flex;
	align-items: center;
	justify-content: space-between;
}

.footer > div:last-child > div {
	width: 24px;
	height: 24px;
	display: flex;
	align-items: center;
	justify-content: center;
}

.footer > div:last-child > div:hover {
	background: rgba(25, 55, 88, 0.04);
}

.footer > div:last-child i {
	width: 16px;
	height: 16px;
	display: inline-block;
	cursor: pointer;
}

.footer .page-scale-percentage {
	cursor: pointer;
	user-select: none;
}

.footer .editor-mode {
	cursor: pointer;
	user-select: none;
}

.footer .paper-size {
	position: relative;
}

.footer .paper-size .options {
	right: 0;
	left: unset;
	box-sizing: content-box;
}

.footer .paper-direction {
	position: relative;
}

.footer .paper-direction .options {
	right: 0;
	left: unset;
}

```
