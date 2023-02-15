```
■window
window
window.self;
window.history;
window.outerHeight;
window.outerWidth;
window.innerHeight;
window.innerWidth;
window.alert("test");
window.confirm("test");
window.prompt("test");
window.print();
window.open();
window.open('https://www.google.com/');
window.open('https://www.google.com/', '_blank');
window.open('https://www.google.com/', '_blank', 'menubar=0,width=500,height=300,top=100,left=100');
window.close();

var testData = "テスト";
console.log(testData);
console.log(window.testData);
window.testData;

var testData = {
  value: "テスト"
}
console.log(testData);
console.log(window.testData);
window.testData;

■console
console.log("一般タイプのログ情報を出力する");
console.info("メッセージタイプのログ情報を出力する");
console.warn("コンソールに警告メッセージを出力する");
console.error("コンソールにエラーメッセージを出力する");
console.trace();

＜------------------- プリミティブ型　-----------------＞
※『数値』、『文字列』、『真偽値』、『undefined』、『null』

＜------------------- オブジェクト型　-----------------＞
※プリミティブに該当しないその他全てのもの
※メソッドとは、オブジェクトがプロパティとして持っている関数
const action = {
  onSelect1: function() {
    console.log("onSelect1");
  },
  onSelect2() {
    console.log("onSelect2");
  },
  onSelect3: () => {
    console.log("onSelect3");
  }
}
action.onSelect1();
action.onSelect2();
action.onSelect3();

const action = {};
action.onSelect1 = function() { console.log("onSelect1") };
action.onSelect2 = () => { console.log("onSelect2") };
action.onSelect1();
action.onSelect2();

＜--------------- 関数リテラル(無名関数)　-------------＞
const user = function() {
  console.log("名前");
};
user();

const user = function() {
  return "名前";
};
const result = user();
console.log(result);

＜--------------------- 即時関数　------------------＞
(function() {
  console.log("結果");
})();

const result = (function (value) {
  return value;
}("結果"));
console.log(result);

＜----------------- コールバック関数　-----------------＞
function firstAction(callback) {
  console.log('firstAction');
  callback();
}
function secondAction() {
  console.log('secondAction');
}
firstAction(secondAction);

function firstAction(callback) {
  for(let i=1; i<=5; i++) {
    callback(i);
  }
}
const secondAction = function(i) {
  console.log(i);
};
firstAction(secondAction);

function firstAction(callback) {
  callback("result1");
  callback("result2");
}
firstAction(function(result) {
  console.log(result);
});

＜--------------------- this　---------------------＞
function user() {
  console.log(this);
}
user();

const user = {
  action: function() {
    console.log(this);
  }
}
user.action();

class BaseClass {
  constructor() {
    this.name = '名前'
  }
  getName() {
    console.log(this);
    console.log(this.name);
  }
}
const baseClass = new BaseClass();
baseClass.getName();

＜------------------ call/apply　------------------＞
※関数.call(this値, 引数1, 引数2…);
※関数.apply(this値, [引数1, 引数2…]);
※引数でthisの参照先を指定できる
※第一引数にnullやundefinedを指定すると、thisはグローバルオブジェクト（ブラウザはwindowオブジェクト）となる
※アロー関数はcall()やapply()の第一引数は無効となる（関数そのものがthisを所持していない）
const baseObj = { name: "工藤" };
function sum(a, b) {
  console.log(this);
  console.log(`${this.name} ${a + b}`);
}
sum.call(baseObj, 10, 20);
sum.call(null, 10, 20);
sum.apply(baseObj, [10, 20]);

const baseObj = { name: "工藤" };
const sum = function(a, b) {
  console.log(this);
  console.log(`${this.name} ${a + b}`);
}
sum.call(baseObj, 10, 20);
sum.call(null, 10, 20);
sum.apply(baseObj, [10, 20]);

■bind
const baseObj = { name: "工藤" };
function sum(a, b) {
  console.log(`${this.name} ${a + b}`);
}
const result = sum.bind(baseObj, 10, 20);
result();

＜------------- arguments（可変長引数）　--------------＞
※引数に渡ってきた全ての値を出力する
※関数の中でのみ利用できるオブジェクト
※アロー関数の中では使用できない
function user(){
  console.log(arguments.length);
  console.log(arguments[0]);
  console.log(arguments[1]);
}
user(1, '名前');

function sum() {
  let sum = 0;
  for (let i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }
  console.log(sum);
}
sum(1, 3, 5);
sum(7, 12, 3, 2, 8);

■Class
class BaseClass {
  constructor(name) {
    this.name = name;
  }
}
const result = new BaseClass("名前");
console.log(result.name);

class BaseClass {
  action() {
    console.log("test")
  }
}
const result = new BaseClass();
result.action();

class BaseClass {
  constructor(name) {
    this.name = name;
  }
  action() {
    console.log(this.name)
  }
}
const result = new BaseClass("名前");
result.action();

class BaseClass {
  static name = "名前";
  static action() {
    console.log("test");
  }
}
console.log(BaseClass.name);
BaseClass.action();

class BaseClass {
  constructor(name) {
    this.#name = name;
  }
  #action() {
    console.log("test")
  }
}
const result = new BaseClass("名前");
console.log(result.name);
result.action();

class BaseClass {
  get getName() {
    return this.resultName
  }
  set setName(value) {
    this.resultName = value;
  }
}
const result = new BaseClass();
result.setName = "名前";
console.log(result.getName);

class BaseClass {
}
BaseClass.prototype.name = "名前";
BaseClass.prototype.action = function() {
  console.log("test");
}
const result = new BaseClass();
console.log(result.name);
result.action();

class ParentClass {
  parentAction() {
    console.log("parentAction");
  }
}
class ChildClass extends ParentClass {
}
const result = new ChildClass();
result.parentAction();

class ParentClass {
  constructor() {
    console.log("parentConstructor");
  }
}
class ChildClass extends ParentClass {
  constructor() {
    super();
  }
}
const result = new ChildClass();

class ParentClass {
  parentAction() {
    console.log("test");
  }
}
class ChildClass extends ParentClass {
  childAction() {
    super.parentAction();
  }
}
const result = new ChildClass();
result.childAction();

■for-in
オブジェクトの処理
let base = {
  test1: 'test1Value',
  test2:'test2Value',
  test3:'test3Value'
}
for (let item in base) {
  console.log(base[item]);
}

■for-of
配列などの処理
let base = ['1','2','3'];
for (let item of base) {
  console.log(item);
}

■スプレッド
const base = [1, 2];
const newArray1 = [...base];
const newArray2 = [...base, 3, 4];
const newArray3 = [...newArray1, ...newArray2];
console.log(newArray1);
console.log(newArray2);
console.log(newArray3);

const base = { a: 1, b: 2 };
const newObj1 = { ...base };
const newObj2 = { ...base, c: 3 };
const newObj3 = { ...newObj1, ...newObj2 };
console.log(newObj1);
console.log(newObj2);
console.log(newObj3);

■typeof
console.log(typeof undefined);    undefined
console.log(typeof null);         object
console.log(typeof NaN);          number
console.log(typeof 11);           number
console.log(typeof 11.1);         number
console.log(typeof "文字");       string
console.log(typeof true);         boolean
console.log(typeof [1, 2]);       object
console.log(typeof {text:"a"});   object
console.log(typeof new Date());   object
console.log(typeof function() {}) function

const result = "文字";
if (typeof result === 'string')

■try-catch
try {
  const result = res;
} catch(e) {
  console.log( e.message );
}

const res = true;
try {
  const result = res;
  if (result) {
    throw new Error('Error');
  }
} catch(e) {
  console.log( e.message );
}

■throw
throw new Error('一般的なエラー全般');
throw new RangeError('数値が有効範囲外の場合のエラー');
throw new ReferenceError('宣言されていない変数のエラー');
throw new SyntaxError('文法エラー');
throw new TypeError('想定されたデータ型でない場合のエラー');

■prototype
const User = function() {
  this.action = function() {
    console.log("Action");
  }
}
const result = new User();
result.action();
  
const User = function(name) {
  this.name = name;
}
User.prototype.getName = function() {
  console.log(this.name);
};
User.prototype.setName = function(name) {
  this.name = name;
}
const result = new User();
result.setName("工藤");
result.getName();

const Action1 = function() {}
const Action2 = function() {}
Action1.prototype.action = function() {
  console.log("Action");
}
Action2.prototype = new Action1();
const result1 = new Action1();
const result2 = new Action2();
result1.action();
result2.action();
```
