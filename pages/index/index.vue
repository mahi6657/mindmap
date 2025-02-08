<template>
	<view class="container">
		<view :class="{left:true, hide: hideFlag}">
			<view class="item" v-for="(item,index) in dataList" :key="index" @click="changeMind(index)">
				{{item.map}}
			</view>
		</view>
		<view :style="{width:flexwidth}">
			<iframe id="myIframe" ref="iframeRef" :src="xurl" frameborder="1" class="iframe" width="100%"
				height="900"></iframe>
		</view>
		<view :class="{btn:true}" :style="{left:btnLeft}">
			<text @click="hideLeft"
				style="color:white;display:inline-block;width: 60px;background-color: gray;">{{btnText}} </text>
			<input v-model="searchText" placeholder="" />
			<button @click="searchMindMap">Search</button>

		</view>
		<view class="share-disable"></view>
	</view>
</template>

<script setup>
	import {
		onMounted,
		ref
	} from "vue";

	let mind = ref();

	// 等待 iframe 加载完成
	const iframeRef = ref(null);

	let xurl = ref('https://xmind.ai/embed/1UtlSKqx?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33')
	let mindMapContainer = ref()
	let dataList = ref([{
			map: 'Map2',
			data: "https://xmind.ai/embed/1UtlSKqx?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map3',
			data: "https://xmind.ai/embed/QKUINPtl?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map4',
			data: "https://xmind.ai/embed/7BMSDzlX?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map5',
			data: "https://xmind.ai/embed/elJnljHM?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map6',
			data: "https://xmind.ai/embed/FdCvmXhO?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map7',
			data: "https://xmind.ai/embed/NHPJKKVO?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map8',
			data: "https://xmind.ai/embed/94KQNlsE?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map9',
			data: "https://xmind.ai/embed/6cMwtRCn?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},
		{
			map: 'Map10',
			data: "https://xmind.ai/embed/bqHP7nG8?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33"
		},

	])


	const xmindUrl = "/aaa/embed/1UtlSKqx?sheet-id=b6a2b210-e0a2-4ce9-a062-bc4387716f33";


	let searchText = ref('')
	let btnText = ref("<<<");
	let hideFlag = ref(false)
	let btnLeft = ref('411px')
	let flexwidth = ref('calc(100% - 401px)')
	const hideLeft = () => {

		if (btnText.value == '<<<') {
			flexwidth.value = '100%'
			btnLeft.value = "10px"
			btnText.value = '>>>'
			hideFlag.value = true;
		} else {
			flexwidth.value = 'calc(100% - 401px)'
			btnLeft.value = "411px"
			btnText.value = '<<<'
			hideFlag.value = false;
		}
	}
	const changeMind = (index) => {
		const url = dataList.value[index].data;
		console.log(url)
		iframeRef.value.src = url;
		xurl.value = url
	}





	const toTest = () => {
		uni.navigateTo({
			url: '/pages/index/test'
		})
	}
</script>

<style>
	.container {
		width: 100%;
		height: 100vh;
		display: flex;
		justify-content: center;
		align-items: center;
		position: relative;
		/* background: linear-gradient(90deg, red, orange); */
	}

	.container .share-disable {}

	.container>.left {
		width: 400px;
		border-right: solid 1px gray;
		display: flex;
		flex-wrap: wrap;
	}

	.container>.left>.item {
		margin: 15px;
		width: 150px;
		height: 150px;
		line-height: 150px;
		text-align: center;
		background: linear-gradient(90deg, #f4f4f4, lightblue);
		border-radius: 18px;
	}

	.container>#map-container {
		/* min-width: 1000px;*/
		width: calc(100% - 401px);
		flex: 1;
		height: 100vh;
		/* background-color: #f4f4f4; */

	}

	.container>#map-container .iframe {
		width: 100%;
		height: 100%;
		border: solid 1px #999;
	}

	.container>.btn {
		position: fixed;
		/* width: 60px; */
		/* height: 30px; */
		text-align: center;
		line-height: 46px;
		top: 10px;
		left: 10px;
		display: flex;
		align-items: center;
		/* background-color: lightgrey; */
		padding-right: 10px;

	}

	.container .share-disable {
		position: fixed;
		top: 197px;
		right: 17px;
		width: 52px;
		height: 40px;
		background-color: white;

	}


	.container uni-input {
		height: 44px;
		background-color: #f4f4f4;
		border: solid 1px lightblue;
	}

	.container>.hide {
		display: none;
	}

	.container .map-canvas {
		background-color: #fff !important;
	}
</style>