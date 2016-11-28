# ECMA6
变量的作用域
这里重要解释一下temporal dead zone，以及块级变量
一、temporal dead zone 暂时死亡区域

  在申明变量之前使用变量：
  function varial (){
    console.log(varValue);
    let varValue =0;
  }
  这里会报错 语法错误 ！ tdz的范围是在使用变量————至申明变量这段区域！
  这一点和之前的说法不一样！
  ECMA5会输出undefined ！
  这里主要是考虑到良好的编码习惯！变量使用要在变量申明之后！
  
  
  
  
二、块级作用域
  这是一个例子：ECMA5
  var tmp = new Date();

  function f() {
    console.log(tmp);
    if (false) {
    var tmp = "hello world";
    console.log(tmp)
    }
  }

  f(); // undefined undefined
  这里的结果都为undefined！因为ECMA5 只存在全局作用域和函数作用域！
  有些同学可能对于上面的例子产生疑惑？为什么是undefined！ 尤其是第一个！
  这里考察的是函数作用域
  在f 函数内 第一次输出tmp 是在函数f 申明变量tmp之后。所以是undefined。
  第二次输出undefined ： 因为if（false）。所以未执行，未申明变量 所以 为undefined。
  
  假设1：没有if判断语句 两次输出都为 当前的时间 Date（）！
  假设2：如果if（）条件改为 true 那么第二次输出为 当前的时间Date（）！第一次为undefined！
  出现这种情况 也就是常说的   变量提升！
  
二、块级作用域 ECMA6
  function f1() {
    let n = 5;
    if (true) {
      let n = 10;  // 这里的let n 只在 if（true）这哥条件语句里面运行！
    }
    console.log(n); // 5  这里的5 是 let =5的结果！
  }
  假设：if 条件语句 内 是 var n =10；那么输出的结果就是 10；
  有些同学可能又要疑惑，let不允许，重复声明同一个变量。
  但是前提是  在相同作用域内。 这里不再同一作用域！
