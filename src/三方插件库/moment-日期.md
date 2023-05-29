# 一. moment 日期格式处理库

1. https://moment.nodejs.cn/

2. npm i moment --save



格式化日期
moment().format('MMMM Do YYYY, h:mm:ss a'); // 五月 30日 2023, 12:30:38 凌晨
moment().format('dddd');                    // 星期二
moment().format("MMM Do YY");               // 5月 30日 23
moment().format('YYYY [escaped] YYYY');     // 2023 escaped 2023
moment().format();                          // 2023-05-30T00:30:38+08:00
相对时间
moment("20111031", "YYYYMMDD").fromNow(); // 12 年前
moment("20120620", "YYYYMMDD").fromNow(); // 11 年前
moment().startOf('day').fromNow();        // 31 分钟前
moment().endOf('day').fromNow();          // 1 天后
moment().startOf('hour').fromNow();       // 31 分钟前
日历时间
moment().subtract(10, 'days').calendar(); // 2023/05/20
moment().subtract(6, 'days').calendar();  // 上周三00:30
moment().subtract(3, 'days').calendar();  // 上周六00:30
moment().subtract(1, 'days').calendar();  // 昨天00:30
moment().calendar();                      // 今天00:30
moment().add(1, 'days').calendar();       // 明天00:30
moment().add(3, 'days').calendar();       // 本周五00:30
moment().add(10, 'days').calendar();      // 2023/06/09
多语言环境支持
moment.locale();         // zh-cn
moment().format('LT');   // 00:30
moment().format('LTS');  // 00:30:38
moment().format('L');    // 2023/05/30
moment().format('l');    // 2023/5/30
moment().format('LL');   // 2023年5月30日
moment().format('ll');   // 2023年5月30日
moment().format('LLL');  // 2023年5月30日凌晨12点30分
moment().format('lll');  // 2023年5月30日 00:30
moment().format('LLLL'); // 2023年5月30日星期二凌晨12点30分
moment().format('llll');