## Example 1
```
var name = 'The Window';
var object = {
  name: 'My Object',
  getNameFunc: function () {
    return function () {
      return this.name;
    };
  }
};
alert(object.getNameFunc() ());
// alert 'The Window'
```

---

## Example 2 
```
var name = 'The Window';
var object = {
  name: 'My Object',
  getNameFunc: function () {
    return function () {
      return this.name;
    };
  }
};
alert(object.getNameFunc() ());
```

---

## Code 1
```
var name = 'The Window';
var object = {
  name: 'My Object',
  getNameFunc: function () {
    return (this.name);
  }
};
var name = object.getNameFunc();
alert(name);
```
- result: 'My Object'

---

## Code 2
```
var name = 'The Window';
var object = {
  name: 'My Object',
  getNameFunc: function () {
    return function () {
      return this.name; //这个this是有上下文的限制的
    };
  }
};
var tmp = object.getNameFunc(); //此时没有执行this.name
var name = tmp(); //这个时候才执行，这时候的this上下文为全局
alert(name);
//alert(object.getNameFunc()())
```
- result: 'The Window'

---
## Code 3
```
var name = 'The Window';
var object = {
  name: 'My Object',
  getNameFunc: function () {
    var that = this;
    return function () {
      return that.name;
    };
  }
};
var tmp = object.getNameFunc(); //这个时候执行了that = this，这里的this上下文是object,所以that指的是object
var name = tmp(); //这个时候执行了that.name
alert(name);
//alert(object.getNameFunc()()); 
```
- result: 'My Object'

---
## Code 4 
```
var n = 1;
function f1() {
  var n = 999;
  nAdd = function () {
    n++;
  }
  function f2() {
    alert(n);
  }
  return f2;
}
var b = f1();
nAdd(); //n = 999+1 = 1000
b(); //弹出 n 的值是 1000 (闭包内的变量n)
alert(n); //弹出n的值是 1 (全局)
```

---
## Code 5 
```
var name = 'The Window';
var object = {
  name: 'My Object',
  getNameFunc: function () {
    alert(this.name); 
    return function () {
      return this.name;
    };
  }
};
alert(object.getNameFunc() ()); 
// first alert 'My Object', then alert 'The Window'
```

---
## Code 6 
```
function ff()
{
  var local = 1;
  this.add1 = function ()
  {
    return ++local;
  };
  this.add2 = function ()
  {
    return ++local;
  }
  this.add3 = function() {
    return ++ local;
  }
}
var local = 50;
var f = new ff();
alert(f.add1()); //2
alert(f.add2()); //3
alert(f.add3());
```

--

## Test 1 (closure in loop)
* [Find the bug of the code, and fixed it , and tell me why? ](http://jsfiddle.net/hfeeki/L35pzeop/)
* [Closure & this](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)