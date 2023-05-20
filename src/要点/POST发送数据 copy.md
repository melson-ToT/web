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


# 二.
const BASE_URL = "http://www.pudge.wang:4000"
const hppt = {
    get(url:string,params:any){
        if(params){
            const arr = Object.keys(params);
            const arr2 = arr.map((item:string)=>item + "=" + params[item]);
            const str = "?" + arr2.join("&")
            url += str
        }
        return fetch(BASE_URL + url)
          .then((response)=>response.json())
          .then((res)=>{
            if(res.status === "0"){
                return res
            }
          })
    },
    post(url:string,data:Object){
        return fetch(BASE_URL + url,{
          method:"post",
          headers:{
            "content-type":"application/json",
          },
          body:JSON.stringify(data),
        })
          .then((response)=>{
            return response.json()
          })
          .then((res)=>{
            if(res.status === "0"){
                return res
            }
          })
    }
}