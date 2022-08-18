## 1. 类命名
使用大写字母作为词的分割，其他的字母均使用小写。
名字的首字母使用大写。
不要使用下划线('_')。
如：`Name、SuperMan、BigClassObject`

## 2. 类属性命名
属性命名应该以字符‘m’为前缀。
前缀‘m’后采用与类命名一致的规则。
‘m’总是在名字的开头起修饰作用，就像以‘r’开头表示引用一样。
如：`mValue、mLongString`等

## 3. 方法的命名
方法的作用都是执行一个动作，达到一个目的。所以名称应该说明方法是做什么的。一般名称的前缀都是有第一规律的，如`is`（判断）、`get`（得到），`set`（设置）。
方法的命名第一个单词的首字母小写，其后单词的首字母大写。。如：
```php
class StartStudy{ //设置类
	$mLessonOne = ""; //设置类属性
	$mLessonTwo = ""; //设置类属性
	function getLessonOne(){ //定义方法，得到属性mLessonOne的值
		...
	}
}
```

## 4. 方法中参数命名
第一个字符使用小写字母。
在首字符后的所有字符都按照类命名规则首字符大写。
如：
```php
class EchoAnyWord{
	function echoWord($firstWord,$secondWord){
		...
	}
}
```

## 5. 引用变量
引用变量要带有‘r’前缀。如：
```php
class Example{
	$mExam = "";
	funciton setExam(&$rExam){
		...
	}
	function getExam(){
	...
	}
}
```

## 6. 变量命名
所有字母都使用小写。
使用‘_’作为每个词的分界。
如：`$msg_error`、`$chk_pwd`等。
临时变量通常被取名为i，j，k，m和n，它们一般用于整型；c，d，e，s 它们一般用于字符型。
实例变量前面需要一个下划线， 首单次小写，其余单词首字母大写。

## 7. 全局变量
全局变量应该带有前缀‘g’。如：`global` `$gTest`。

## 8. 常量、全局常量
常量、全局常量，应该全部使用大写字母，单词之间用‘_’来分割。如
```php
define('DEFAULT_NUM_AVE',90);
```
```php
define('DEFAULT_NUM_SUM',500);
```

## 9. 静态变量
静态变量应该带有前缀‘s’。如：
`state $sStatus = 1;`

## 10. 函数命名
所有的名称都使用小写字母，多个单词使用‘_’来分割。如：
```php
function this_good_idear(){
	...
}
```
以上的各种命名规则，可以组合一起来使用，如：
```php
class OtherExample{
	$msValue = ""; //该参数既是类属性，又是静态变量
}
```
