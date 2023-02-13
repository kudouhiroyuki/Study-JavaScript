```
■window
<script></script>の内では window.は省略できる（ window.alert() ⇨ alert() ）
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

■this
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

■オブジェクト
const action = {
  onSelect: () => {
    console.log("onSelect");
  }
}
action.onSelect();

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
