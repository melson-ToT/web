##### 一.利用正则，将地址栏数据对象的某些提取出来 

2. eval()
         ----将字符串格式的对象转为对象
#       var arr = 'https://www.baidu.com?a=1&b=2&c=3&d=4'
                  
#       arr = arr.substring(arr.indexOf('?')+1)
                 substring截取字符串,从?开始到结束，+1代表向后一位 

#       console.log(arr)  //    a=1&b=2&c=3&d=4
           
#       console.log(eval('({'+arr.replace(/&/g,',').replace(/=/g,':')+'})'));
                    正则（） { 'arr内替换    &为，      替换    =为：   }
#               打印的结果arr={'a:1','b:2','c:3','d:4'}

# 二.将密码设置为隐藏，点击图片时，则密码显示，反复点击时，来回切换
    let flag = false                  1.给这个标记为布尔值，为假
    img.onclick = function(){         2.点击图片时
      flag = !flag                    3.标记的布尔值，取反
      if(flag){                       4.如果标记为反
        input[1].type='text'          5.input的属性为显示
      } else {
        input[1].type='password'      6.否则input的属性为隐藏
      }
    }



# 三。登录页面
<body>
    <fieldset style="width: 800px;margin:0 auto;">
        <legend>用户注册：</legend>
        <form action="success.html">
            <p><label for="">用户名：</label><input type="text" class="username"> <span></span></p>
            <p><label for="">手机号：</label><input type="text" class="tel"> <span></span></p>
            <p><label for="">密 码：</label><input type="password" class="password"> <span></span></p>
            <p><input type="submit" value="提交注册" class="btn"></p>
        </form>
    </fieldset>
</body>
 
</html>
<script>
    var oForm = document.querySelector('form');
    var oBtn = document.querySelector('.btn');
    var oUsername = document.querySelector('.username');
    var oTel = document.querySelector('.tel');
    var oPassword = document.querySelector('.password');
    var aSpan = document.querySelectorAll('form span'); //获取多个span
 
 
 
 
    // 表单注册
    // 一.form+submit进行页面的跳转，跳转是由form发起的，通过onsubmit事件发起。
    // oForm.onsubmit = function() { //阻止默认行为，不会跳转。
    //     return false;
    // }
 
    // 1.表单没有通过的情况下，禁用注册按钮
    oBtn.disabled = true;
 
    // 准备标记，检测用户名是否完全通过验证
    var usernameflag = false;
    var telflag = false;
    var passwordflag = false;
 
 
    // 二.用户名的表单验证
    // 规则：设置后不可更改，中英文均可，最长14个英文或7个汉字
    // 1.得到焦点产生提示信息。
    oUsername.onfocus = function() {
        aSpan[0].innerHTML = '设置后不可更改，中英文均可，最长14个英文或7个汉字';
        aSpan[0].style.color = '#333';
    };
 
    // 2.失去焦点进行验证。
    oUsername.onblur = function() {
        //第一步判断是否为空
        if (this.value !== '') {
            //第二步判断长度:将中文替换成对应的两个英文字符，再进行长度统计
            var len = this.value.replace(/[\u4e00-\u9fa5]/g, '**').length;
            if (len <= 14) {
                //第三步检测中英文
                var reg = /^[a-zA-Z\u4e00-\u9fa5]+$/;
                if (reg.test(this.value)) {
                    aSpan[0].innerHTML = '√';
                    aSpan[0].style.color = 'green';
                    usernameflag = true;
                } else { //用户名格式有误
                    aSpan[0].innerHTML = '用户名格式有误';
                    aSpan[0].style.color = 'red';
                    usernameflag = false;
                }
 
            } else { //用户名长度有问题
                aSpan[0].innerHTML = '用户名长度有问题';
                aSpan[0].style.color = 'red';
                usernameflag = false;
            }
        } else { //用户名为空
            aSpan[0].innerHTML = '用户名不能为空';
            aSpan[0].style.color = 'red';
            usernameflag = false;
        }
        check(); //检测按钮是否可以点击。
    };
 
 
 
    // 三.手机号码的表单验证
    // 1.得到焦点产生提示信息。
    oTel.onfocus = function() {
        aSpan[1].innerHTML = '请输入正确的11位手机号码';
        aSpan[1].style.color = '#333';
    };
    // 2.失去焦点进行验证。
    oTel.onblur = function() {
        //第一步判断是否为空
        if (this.value !== '') {
            //第二步手机号验证
            var reg = /^1[3-9]\d{9}$/;
            if (reg.test(this.value)) {
                aSpan[1].innerHTML = '√';
                aSpan[1].style.color = 'green';
                telflag = true;
            } else {
                aSpan[1].innerHTML = '手机号格式有误';
                aSpan[1].style.color = 'red';
                telflag = false;
            }
        } else {
            aSpan[1].innerHTML = '手机号不能为空';
            aSpan[1].style.color = 'red';
            telflag = false;
        }
        check();
    }
 
 
 
 
    // 四.密码验证
    //匹配规则：长度8-20个字符，数字字母特殊符号组成，两种以上的字符，弱中强的判断。
    //弱:一种字符
    //中:二种或者三种字符
    //强:四种字符
    // 1.得到焦点产生提示信息。
    oPassword.onfocus = function() {
        aSpan[2].innerHTML = '请输入8-20个数字字母特殊符号组成的密码';
        aSpan[2].style.color = '#333';
    };
    // 2.边输入边检查弱中强
    // oninput:只要文本框的内容发生改变，立刻触发。
    oPassword.oninput = function() {
        var reg1 = /\d+/;
        var reg2 = /[a-z]+/;
        var reg3 = /[A-Z]+/;
        var reg4 = /[!@#$%^&*]+/;
        var count = 0;
        if (reg1.test(this.value)) { //存在数字
            count++;
        }
        if (reg2.test(this.value)) { //存在小写字母
            count++;
        }
        if (reg3.test(this.value)) { //存在大写字母
            count++;
        }
        if (reg4.test(this.value)) { //存在特殊符号
            count++;
        }
        switch (count) {
            case 1:
                aSpan[2].innerHTML = '弱';
                aSpan[2].style.color = 'red';
                passwordflag = false;
                break;
            case 2:
            case 3:
                aSpan[2].innerHTML = '中';
                aSpan[2].style.color = 'orange';
                passwordflag = true;
                break;
 
            case 4:
                aSpan[2].innerHTML = '强';
                aSpan[2].style.color = 'green';
                passwordflag = true;
                break;
        }
    };
 
    // 3.失去焦点进行验证。
    oPassword.onblur = function() {
        if (this.value !== '') {
            if (this.value.length >= 8 && this.value.length <= 20) {
                // 等待密码弱中强的结果进行最后的判断
                if (passwordflag) {
                    aSpan[2].innerHTML = '√';
                    aSpan[2].style.color = 'green';
                }
            } else {
                aSpan[2].innerHTML = '密码长度有误';
                aSpan[2].style.color = 'red';
            }
        } else {
            aSpan[2].innerHTML = '密码不能为空';
            aSpan[2].style.color = 'red';
        }
        check();
    };
 
    // 按钮是否可以点击函数
    function check() {
        if (usernameflag && telflag && passwordflag) {
            oBtn.disabled = false; //可用
        } else {
            oBtn.disabled = true; //禁用
        }
    }
 
 
    function inputMethod(value) {
        //强:
        var reg1 = /^(?=.*[A-Z])(?=.*[a-z])(?=.*[0-9])(?=.*\W).{8,20}$/g;
        //中:
        var reg2 = /^(((?=.*[A-Z])(?=.*[a-z]))|((?=.*[A-Z])(?=.*[0-9]))|((?=.*[a-z])(?=.*[0-9]))|((?=.*[a-z])(?=.*\W))|((?=.*[0-9])(?=.*\W))|((?=.*[A-Z])(?=.*\W))).{8,20}$/g;
        //弱:
        var reg3 = /.{8,20}/g;
 
        if (reg1.test(value)) {
            console.log('强');
        } else if (reg2.test(value)) {
            console.log('中');
        } else if (reg3.test(value)) {
            console.log('弱');
        }
    }
</script>