# 一：布局和注册页面
1.准备三个页面：
             登录页面
             注册页面
             首页

2.准备注册页面的布局：

2.1.注册页面的布局(后端约定 - 接口约定)
注册接口：http://localhost:8888/users/register
请求方式：post
携带数据：
username    必填string  用户名
password    必填string  密码
rpassword   必填string  重复密码(必须和密码一致)
nickname    必填string  用户昵称
 
2.2.登录页面的布局
登录接口：http://localhost:8888/users/login
请求方式：post
携带数据：
username    必填string  用户名
password    必填string  密码
 
 
2.3.首页布局
如果没有登录，显示你好请登录，免费注册

封装好的发送请求           
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>注册页面</title>
</head>
<body>
<fieldset>
  <legend>用户注册:</legend>
  <p><label for="">用户昵称</label><input type="text" class="nic"><span class="noc" style="color: red;"></span></p>
  <p><label for="">密&emsp;&emsp;码</label><input type="text" class="mima"></p>
  <p><label for="">密码重复</label><input type="text" class="mimas"><span class="nom" style="color: red;">密码一致</span></p>
  <p><button>用户注册</button></p>
  </fieldset>
</body>
</html>
<script src="promise.js"></script>
<script>
  const nic = document.querySelector('.nic')
  const noc = document.querySelector('.noc')
  const mima = document.querySelector('.mima')
  const mimas = document.querySelector('.mimas')
  const nom = document.querySelector('.nom')
  const button = document.querySelector('button')
    button.onclick = function () {
        $ajax({
          url: 'api/register/',
          data:{"username":"dsdfd","name":"vdv","email":"cscsa@qq.com","password":"e10adc3949ba59abbe56e057f20f883e","repassword":"e10adc3949ba59abbe56e057f20f883e","code":"","uuid":"b6da947bdb1e7f35f34c9971ed79df6b62017d2d","idValueC":"","idKeyC":"b6da947bdb1e7f35f34c9971ed79df6b62017d2d"}
        }).then((res)=>{
          if(res.code===200){
          }else{
            noc.innerHTML = '用户重名'
            nic.value = ''
            mima.value = ''
            mimas.value = ''
          }
        })
      }
</script>

3.准备登录页面的布局：
            登录页面的布局（后端约定的接口）
  <body>
    <fieldset>
      <legend>用户注册:</legend>
      <p><label for="">用户昵称</label><input type="text" class="nic"><span class="noc">不能重名</span></p>
      <p><label for="">密&emsp;&emsp;码</label><input type="text" class="mima"></p>
      <p><input type="button" value ="用户登录"></p>
    </fieldset>
  </body>
</html>
<script src="promise.ji.html"></script>
<script>
  const nic = document.querySelector('.nic')
  const noc = document.querySelector('.noc')
  const mima = document.querySelector('.mima')
  const nom = document.querySelector('.nom')
  const button = document.querySelector('button')
    button.onclick = function () {
        $ajax({
          url: 'api/userInfo/',
          nic:nic.valu,
          mima:nic.mima,
          mimas:nic.mimas
        }).then((res)=>{
            console.log(res)
             if(res.code===200){//登录成功，存储token，并跳转到首页
              localStorage.setItem('authorization',res.token)//（存储token）非常重要

              localstorage.setitem('id',res.id)

              localStorage.setItem()方法用于在本地存储中设置值。该方法接受两个参数:键和值。

            }else{
              noc.innerHTML = '用户名和密码错误'
            }
        })
      }
</script>



4.首页布局
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>网站首页</title>
  </head>
  <body>
    <div class="logstr1" style="display: block">
      <a href="file:///D:/1/html/%E7%BB%83%E4%B9%A0%202.html">你好请登录</a>,<a
        href="file:///D:/1/html/%E7%BB%83%E4%B9%A0%201.html"
        >免费注册</a
      >
    </div>
    <div class="logstr2" style="display: none">
      <a href="">你好已登录</a>,<a href="">欢迎使用</a>
    </div>
  </body>
</html>
<script src="promise.shouye.js"></script>
<script>
  let id = localStorage.getItem("id");
  let token = localStorage.getItem("token");
  const logstr1 = document.querySelector(".logstr1");
  const logstr2 = document.querySelector(".logstr2");
  if (id && token) {     1.如果有id和token
    $ajax({              2.发送请求
      url: "http://47.122.0.39:8000" / +路径, 拿后端给的路径
      data: {            
        id: id,
        token: token,
      }
    }).then((res)=>{                 3.获取数据
      console.log(res);
      if(res.coad===200){            4.如果，返回的coad等于200
        logstr1.style.display = "none"  
        logstr2.style.display = "block"
        a2.innerHTML = res.retName   5.a标签的内容 = 接口登录内的名字
      }
    })
  }else{
    logstr1.style.display = "block"
    logstr2.style.display = "none"
  }
</script>


# 二.注册页面的流程
1.准备好布局的结构
2.通过ajax将用户注册的信息提交给后端(考虑表单验证)，后端返回对应的信息
3.根据后端返回的结构，判断是否通过注册
4.如果注册成功，跳转到登录页面：location.href="http://www.jd.com"

# 三.登录页面实现流程
1.准备好布局的结构
2.通过ajax将用户名和密码信息提交给后端，后端拿到用户名和密码去和数据库的用户名和密码进行匹配，返回的结构给前端
3.拿到返回的结果，确定是否登录成功
4.如果注册登录，一定要存储后端传来的token（本地存储）

# 四.koken
1.http的无状态通讯(浏览器到服务器的通讯)
无状态是指，当浏览器给服务器发送请求的时候，服务器响应客户端请求。
但是当同一个浏览器再次发送请求给服务器的时候，服务器并不知道他就是刚才的那个浏览器。
简单的说，就是服务器不会去记得你，所以就是http的无状态协议。
 
2.token
登录的流程：客户端对服务器发起请求，携带用户名和密码，后端拿到前端的用户名和密码，去和数据库里面的用户信息进行对比，判断用户名和密码是否正确，做出响应。
为了减少服务端频繁去进行上面的操作，引入token。
Token的目的是为了减轻服务器的压力，减少频繁的查询数据库，使服务器更加健壮。
 
什么是token
token的意思是“令牌”，是服务器生成的一段加密字符串，然后返回给客户端
第一次登录，传入用户名和密码，后端在第一次登录成功之后，给token，下次不需要再给用户名和密码，用后端给的token去登录
 
后端根据用户的信息生成的一段秘钥，登录成功的时候将秘钥返回给前端，下次前端再登录(没有超过约定登录的时间)，无需用户名和密码，
直接将后端传递token发送给后端，后端匹配，匹配成功，用户登录成功，否则登录失败。
 
注意每次登录都有时间限定，如果过了时间重新登录，如果时间没有过，利用token进行匹配登录，任何页面都可以发送token进行登录。
 
 
# 四.首页实现流程:（非常重要）
                 localStorage.setItem('authorization',res.token)
                     存储本地             后端定义        token

                 localStorage.getItem('authorization',res.token)
                     获取本地             后端定义        token

                 localStorage.setItem('authorization',res.id)
                     存储本地             后端定义        id

                 localStorage.getItem('authorization',res.id)
                     获取本地             后端定义        id



1.首页需要用户的信息，但是不能在登录页面去，必须由首页去登录(直接传递token实现)，去获取用户的信息
2.拿到用户名等信息 - 获取用户详细信息的接口 - http://localhost:8888//users/info - 传递id
3.将token传递给后端，利用设置请求头进行传递。默认设置了字段：authorization,获取用户信息
4.显示用户信息
注意：如果修改登录保持的时间，服务器必须重启

