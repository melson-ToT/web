js-cookie的使用方法
# 一、先下载

npm install --save js-cookie



# 二、引入
安装好js-cookie插件后，在我们需要处理cookie的地方，简单的通过import引入就可以使用了

import Cookies from 'js-cookie'



# 三、js-cookie的添加 获取 删除

添加cookie

1. 创建一个名称为name，对应值为value的cookie，由于没有设置失效时间，默认失效时间为该网站关闭时
Cookies.set(name, value)

2. 创建一个有效时间为7天的cookie
Cookies.set(name, value, { expires: 7 })

3. 创建一个带有路径的cookie
Cookies.set(name, value, { path: '' })

4. 创建一个value为对象的cookie
const obj = { name: 'ryan' }
Cookies.set('user', obj)



# 四、js-cookie的添加 获取 删除
获取cookie

1. 获取指定名称的cookie
Cookies.get(name) // value

2. 获取value为对象的cookie
const obj = { name: 'ryan' }
Cookies.set('user', obj)
JSON.parse(Cookies.get('user'))

3. 获取所有cookie
Cookies.get()



# 四、js-cookie的添加 获取 删除
删除cookie

1. 删除指定名称的cookie
Cookies.remove(name) // value

2. 删除带有路径的cookie
Cookies.set(name, value, { path: '' })
Cookies.remove(name, { path: '' })





一、下载cookie

npm install js-cookie
二、当前页面引用cookie

import Cookies from "js-cookie";
三、cookie在当前的使用(方法一)

// 组件中使用
// 写入cookie
Cookies.set('name', 'value')
// 读取
Cookies.get('name') // => 'value'
Cookies.get('nothing') // => undefined
// 读取所有可见的cookie
Cookies.get()
// 删除某项cookie值
Cookies.remove('name')
四、cookie在全局使用（方法二）

main.js

import Cookies from 'js-cookie'
五、cookie设置过期时间

//1、存cookie  set方法支持的属性有 ：  expires->过期时间    path->设置为指定页面创建cookie   domain-》设置对指定域名及指定域名的子域名可见  secure->值有false和true ,表示设置是否只支持https,默认是false
Cookies.set('key', 'value');  //创建简单的cookie
Cookies.set('key', 'value', { expires: 27 });//创建有效期为27天的cookie
Cookies.set('key', 'value', { expires: 17, path: ''  }); //可以通过配置path,为当前页创建有效期7天的cookie

//2、取cookie
Cookies.get('key'); // 获取指定key 对应的value
Cookies.get(); //获取所有value

//3、删除cookie
Cookies.remove('key');//删除普通的cookie
Cookies.remove('name', { path: '' }); // 删除存了指定页面path的cookie
注意：如果存的是对象，如： userInfo = {age:111,score:90};  Cookie.set('userInfo',userInfo)

取出来的userInfo需要进行JSON的解析,解析为对象：let res = JSON.parse( Cookie.get('userInfo') );

当然你也可以使用：Cookie.getJSON('userInfo');
Cookies.get('name'); // => '{"foo":"bar"}'
Cookies.get(); // => { name: '{"foo":"bar"}' }
//-------------------------------------------------------//
Cookies.getJSON('name'); // => { foo: 'bar' }
Cookies.getJSON(); // => { name: { foo: 'bar' } }
举例二：
背景：业务需要在前端进行数据的缓存，到期就删除再进行获取新数据。

前端设置数据定时失效的可以有下面2种方法：
1、当数据较大时，可以利用localstorage，存数据时候写入一个时间，获取的时候再与当前时间进行比较
2、如果数据不超过cookie的限制大小，可以利用cookie比较方便，直接设置有效期即可。
/--------------------------------------------------------------------------------------/
利用localstorage实现：步骤
1.存储数据时加上时间戳
在项目开发中，我们可以写一个公用的方法来进行存储的时候加上时间戳

//export抛出
export function setLocalStorageAndTime (key, value) {
 window.localStorage.setItem(key, JSON.stringify({ data: value, time: new Date().getTime() }))
}
项目中：
存储、

// 有数据再进行存储
  setLocalStorageAndTime('XXX', {name: 'XXX'})
读取、

// 判断是否返回为null或者失效
getLocalStorageAndTime('XXX', 86400000)
获取数据时与当前时间进行比较、

export function getLocalStorageAndTime (key, exp = 86400000) {
 // 获取数据
 let data = window.localStorage.getItem(key)
 if (!data) return null
 let dataObj = JSON.parse(data)
 // 与过期时间比较
 if (new Date().getTime() - dataObj.time > exp) {
  // 过期删除返回null
  removeLocalStorage(key)
  console.log('信息已过期')
  return null
 } else {
  return dataObj.data
 }
}
//----------------------------------------------------------------------------------------/
利用cookie实现
js-cookie 的示例中只有以天为单位的有效期：

Cookies.set('name', 'value', { expires: 7 }); // 7 天后失效
官方文档只要设置天数，没有时分秒，这样我们想设置更小单位的时候无法下手，其实也可以设置时间戳来处理时间的，下面这种方式可以设置任意单位的有效期：

let seconds = 10;
let expires = new Date(new Date() * 1 + seconds * 1000);
Cookies.set('username', 'tanggaowei', { expires: expires }); // 10 秒后失效
贴上利用js-cookie的封装, 记得 npm i js-cookie

import Cookies from 'js-cookie'
 
/*
* 设置cookies
* */
export function getCookies (key) {
 return Cookies.get(key)
}
/*
* 设置Cookies
* */
export function setCookies (key, value, expiresTime) {
 let seconds = expiresTime
 let expires = new Date(new Date() * 1 + seconds * 1000)
 return Cookies.set(key, value, { expires: expires })
}
/*
* 移除Cookies
* */
export function removeCookies (key) {
 return Cookies.remove(key)
}
域domain与路径path
默认值：
path: ‘/’
前言：

domain表示的是cookie所在的域，默认为请求的地址，如网址为www.jb51.net/test/test.aspx，那么domain默认为www.jb51.net。而跨域访问，如域A为t1.test.com，域B为t2.test.com，那么在域A生产一个令域A和域B都能访问的cookie就要将该cookie的domain设置为.test.com；如果要在域A生产一个令域A不能访问而域B能访问的cookie就要将该cookie的domain设置为t2.test.com。

path表示cookie所在的目录，asp.net默认为/，就是根目录。在同一个服务器上有目录如下：/test/,/test/cd/,/test/dd/，现设一个cookie1的path为/test/，cookie2的path为/test/cd/，那么test下的所有页面都可以访问到cookie1，而/test/和/test/dd/的子页面不能访问cookie2。这是因为cookie能让其path路径下的页面访问。

cookie.set()更多参数
语法：
cookies.set（名称，[值]，[options]）
更多options的参数配置：

maxAge：一个数字，表示自Date.now()到期起的毫秒数

expires：一个Date对象，指示cookie的过期日期（默认在会话结束时过期）。默认：天

path：一个字符串，指示cookie的路径（/默认情况下）。

domain：一个字符串，指示cookie的域（无默认值）。

secure：一个布尔值，指示cookie是否仅通过HTTPS发送（false默认情况下，对于HTTP，true默认情况下，对于HTTPS）。在下面阅读有关此选项的更多信息。
httpOnly：一个布尔值，指示cookie是否仅通过HTTP（S）发送，并且不提供给客户端JavaScript（true默认情况下）。

sameSite：布尔值或字符串，指示cookie是“相同站点” cookie（false默认情况下）。可以将其设置为’strict’，‘lax’或true（映射到’strict’）。








2、存入
复制代码
// Create a cookie, valid across the entire site:  
Cookies.set('name', 'value');  
   
// Create a cookie that expires 7 days from now, valid across the entire site:  
Cookies.set('name', 'value', { expires: 7 });  
   
// Create an expiring cookie, valid to the path of the current page:  
Cookies.set('name', 'value', { expires: 7, path: '' });  
复制代码
3、取出

复制代码
// Read cookie:  
Cookies.get('name'); // => 'value'  
Cookies.get('nothing'); // => undefined  
   
// Read all visible cookies:  
Cookies.get(); // => { name: 'value' }  
复制代码
4、删除

复制代码
// Delete cookie:  
Cookies.remove('name');  
   
// Delete a cookie valid to the path of the current page:  
Cookies.set('name', 'value', { path: '' });  
Cookies.remove('name'); // fail!  
Cookies.remove('name', { path: '' }); // removed!  
Cookies.remove('name', { path: '', domain: '' }); // removed! 
复制代码
5、命名空间

如果担心不小心修改掉Cookies中的数据，可以用noConflict方法定义一个新的cookie。

var Cookies2 = Cookies.noConflict();
Cookies2.set('name', 'value');
 

6、set方法的参数解释

第一个：name,必选参数，这个是cookie的变量名  
第二：value,可选参数，这个cookie变量的值
第三个：expire,可选参数，这个是用来设置cookie变量保存的时间  
第四个：path,cookie的有效范围，这个参数是下一个参数domain基础上的有效范围，如果path设置为”/”，那就是在整个 domain都有效，比如setcookie(“user”,”php”,time()+3600,”/”),这样我们domain下的任何目录，任何文件都可以通过$_COOKIE['user']来调用这个cookie变量的值。如果path设置为”/test”,那么只在domain下的/test 目录及子目录才有效，比如domain下有两个目录: test1,test2,我们设置为setcookie(“user”,”php,time()+3600,”/test1″)，那么只有test1目录下才能通过$_COOKIE['user']调用user这个cookie变量的值，test2目录下获取不到。  
第五个：domain,cookie有效的域名，如果domain,设置为googlephp.cn，那么在googlephp.cn下的所有子域都有效。假设googlephp.cn有两个子域，php.googlephp.cn，css.googlephp.cn，我们设置为 setcookie(“user”,”php”,time()+3600,”/”,”php.googlephp.cn”),那么只有在 php.googlephp.cn这个子域下才能获取user这个cookie变量的值. 再举一个例子：setcookie(“user”,”php”,time()+3600,”/test”,”php.googlephp.cn”),那么只有在php.googlephp.cn这个子域下的test目录下才能获取user这个cookie变量的值.  
例如设成".hanj.com"则在.hanj.com下的所有服务器下的文件都可以调用cookie，在hanj的所有子域名下都可以访问，实现跨站点通信
Cookies.set("token", v, { domain: '.guohua.com' });
注意：通过domain设置的cookie清除的时候也必须使用domain清除
Cookies.remove("token", { domain: '.guohua.com' });
secure
true或false，表示cookie传输是否仅支持https。默认为不要求协议必须为https。:默认情况下为false;用http协议不安全传输;true:用https等协议安全传输.