# 一.
const axios from 'axios'

import { showToast } from 'vant';  // vue 的 组件UI库  vant(使用与移动端)

$request = (.......axios的全局请求封装)

const data = {
	id: 1,
	type: 2
}

const function xxxx = (data) => {
	$request({
		url: 'http://wswwww',
		methods: 'post',
		data: data
	}).then(res => {
	  if (res.code === 200) {
		showToast({
			message: res.message,
			position: 'top',
		});
	  }
	})
}