# 自己的JavaScript武器库


## 1.前言
大家在开发的时候应该知道，有很多常见的实例操作。比如数组去重，关键词高亮，打乱数组等。这些操作，代码一般不会很多，实现的逻辑也不会很难，下面的代码，我解释就不解释太多了，打上注释，相信大家就会懂了。但是，用的地方会比较，如果项目有哪个地方需要用，如果重复写的话，就是代码沉余，开发效率也不用，复用基本就是复制粘贴！这样是一个很不好的习惯，大家可以考虑一下把一些常见的操作封装成函数，调用的时候，直接调用就好！


- 1.前言
- 2.字符串操作
- 2-1去除字符串空格
- 2-2字母大小写切换
- 2-3字符串循环复制
- 2-4字符串替换
- 2-5 字符串替换*
- 2-6检测字符串
- 2-7 检测密码强度
- 2-8随机码（toString详解）
- 2-9查找字符串出现次数
- 2-10 过滤字符串
- 2-11格式化处理字符串
- 2-12找出最长单词
- 2-13现金额转大写
- 3.数组操作
- 3-1数组去重
- 3-2数组顺序打乱
- 3-3数组最大值最小值
- 3-4数组求和，平均值
- 3-5从数组中随机获取元素
- 3-6回数组字符串一个元素出现的次数
- 3-7数组/字符串出现最多的几次元素和出现次数
- 3-8得到n1-n2下标的数组
- 3-9筛选数组
- 3-10 获取对象数组某些项
- 3-11 排除对象数组某些项
- 3-12 对象数组排序
- 3-13 判断两个数组是否相等
- 4.基础DOM操作
- 4-1检测对象是否有哪个类名
- 4-2 添加类名
- 4-3删除类名
- 4-4替换类名("被替换的类名","替换的类名")
- 4-5设置样式
- 4-6设置文本内容
- 4-7显示隐藏
- 4-8获取滚动条距顶部的距离
- 4-9获取元素的距离文档的位置
- 5-0获取元素的距离文档的位置
- 5.1 滚动条平滑滚动指定位置
- 5 Random 随机值
- 5-1 随机生成颜色
- 5-2 生成指定范围随机数
- 6 获取，设置url参数
- 6-1 url参数转对象
- 6-2 设置url参数
- 6-3 获取url参数
- 获取指定url参数
- 7 Time 时间
- 7-1 到某一个时间的倒计时
- 7-2 时间戳转日期
- 8 封装ajax函数
- 9 图片懒加载
- 10 关键词加标签/高亮
- 11 数据类型判断
- 12 手机类型判断
- 13 函数节流
- 14 常用正则
- 15 其他拓展-不断添加
- 15-1 多张无缝轮播


## 2.字符串操作
### 2-1去除字符串空格
```
//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
//trim('  1235asd',1)
//result：1235asd
//这个方法有原生的方案代替，但是考虑到有时候开发PC站需要兼容IE8，所以就还是继续保留

trim: function (str, type) {
    switch (type) {
        case 1:
            return str.replace(/\s+/g, "");
        case 2:
            return str.replace(/(^\s*)|(\s*$)/g, "");
        case 3:
            return str.replace(/(^\s*)/g, "");
        case 4:
            return str.replace(/(\s*$)/g, "");
        default:
            return str;
    }
}

```

### 2-2字母大小写切换
```
/*type
 1:首字母大写
 2：首页母小写
 3：大小写转换
 4：全部大写
 5：全部小写
 * */
//changeCase('asdasd',1)
//result：Asdasd

changeCase: function (str, type) {
    function ToggleCase(str) {
        var itemText = ""
        str.split("").forEach(
            function (item) {
                if (/^([a-z]+)/.test(item)) {
                    itemText += item.toUpperCase();
                } else if (/^([A-Z]+)/.test(item)) {
                    itemText += item.toLowerCase();
                } else {
                    itemText += item;
                }
            });
        return itemText;
    }
    switch (type) {
        case 1:
            return str.replace(/\b\w+\b/g, function (word) {
                return word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
            });
        case 2:
            return str.replace(/\b\w+\b/g, function (word) {
                return word.substring(0, 1).toLowerCase() + word.substring(1).toUpperCase();
            });
        case 3:
            return ToggleCase(str);
        case 4:
            return str.toUpperCase();
        case 5:
            return str.toLowerCase();
        default:
            return str;
    }
}
 
```
### 2-3字符串循环复制
```
//repeatStr(str->字符串, count->次数)
//repeatStr('123',3)
//"result：123123123"

repeatStr: function (str, count) {
    var text = '';
    for (var i = 0; i < count; i++) {
        text += str;
    }
    return text;
}
 
```

### 2-4字符串替换

```
//replaceAll('这里是上海，中国第三大城市，广东省省会，简称穗，','上海','广州')
//result："这里是广州，中国第三大城市，广东省省会，简称穗，"

replaceAll: function (str, AFindText, ARepText) {
    raRegExp = new RegExp(AFindText, "g");
    return str.replace(raRegExp, ARepText);
}
 
```
### 2-5 字符串替换* 
```
//字符替换*
//replaceStr(字符串,字符格式, 替换方式,替换的字符（默认*）)
//replaceStr('18819322663',[3,5,3],0)
//result：188*****663
//replaceStr('asdasdasdaa',[3,5,3],1)
//result：***asdas***
//replaceStr('1asd88465asdwqe3',[5],0)
//result：*****8465asdwqe3
//replaceStr('1asd88465asdwqe3',[5],1,'+')
//result："1asd88465as+++++"

replaceStr: function (str, regArr, type, ARepText) {
    var regtext = '',
        Reg = null,
        replaceText = ARepText || '*';
    //repeatStr是在上面定义过的（字符串循环复制），大家注意哦
    if (regArr.length === 3 && type === 0) {
        regtext = '(\\w{' + regArr[0] + '})\\w{' + regArr[1] + '}(\\w{' + regArr[2] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[1]);
        return str.replace(Reg, '$1' + replaceCount + '$2')
    }
    else if (regArr.length === 3 && type === 1) {
        regtext = '\\w{' + regArr[0] + '}(\\w{' + regArr[1] + '})\\w{' + regArr[2] + '}'
        Reg = new RegExp(regtext);
        var replaceCount1 = this.repeatStr(replaceText, regArr[0]);
        var replaceCount2 = this.repeatStr(replaceText, regArr[2]);
        return str.replace(Reg, replaceCount1 + '$1' + replaceCount2)
    }
    else if (regArr.length === 1 && type === 0) {
        regtext = '(^\\w{' + regArr[0] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
    else if (regArr.length === 1 && type === 1) {
        regtext = '(\\w{' + regArr[0] + '}$)'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
}
 
```

### 2-6检测字符串
```
//检测字符串
//checkType('165226226326','phone')
//result：false
//大家可以根据需要扩展

checkType: function (str, type) {
    switch (type) {
        case 'email':
            return /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/.test(str);
        case 'phone':
            return /^1[3|4|5|7|8][0-9]{9}$/.test(str);
        case 'tel':
            return /^(0\d{2,3}-\d{7,8})(-\d{1,4})?$/.test(str);
        case 'number':
            return /^[0-9]$/.test(str);
        case 'english':
            return /^[a-zA-Z]+$/.test(str);
        case 'text':
            return /^\w+$/.test(str);
        case 'chinese':
            return /^[\u4E00-\u9FA5]+$/.test(str);
        case 'lower':
            return /^[a-z]+$/.test(str);
        case 'upper':
            return /^[A-Z]+$/.test(str);
        default:
            return true;
    }
}
 
```

### 2-7 检测密码强度
```
//checkPwd('12asdASAD')
//result：3(强度等级为3)

checkPwd: function (str) {
    var nowLv = 0;
    if (str.length < 6) {
        return nowLv
    }
    if (/[0-9]/.test(str)) {
        nowLv++
    }
    if (/[a-z]/.test(str)) {
        nowLv++
    }
    if (/[A-Z]/.test(str)) {
        nowLv++
    }
    if (/[\.|-|_]/.test(str)) {
        nowLv++
    }
    return nowLv;
}
 
```
### 2-8随机码（toString详解）
```
//count取值范围0-36
//randomWord(10)
//result："2584316588472575"
//randomWord(14)
//result："9b405070dd00122640c192caab84537"
//randomWord(36)
//result："83vhdx10rmjkyb9"

randomWord: function (count) {
    return Math.random().toString(count).substring(2);
}
 
```
### 2-9查找字符串出现次数
```
//var strTest='sad44654blog5a1sd67as9dablog4s5d16zxc4sdweasjkblogwqepaskdkblogahseiuadbhjcibloguyeajzxkcabloguyiwezxc967'
//countStr(strTest,'blog')
//result：6

countStr: function (str, strSplit) {
    return str.split(strSplit).length - 1
}
 
```
### 2-10 过滤字符串 
```
//过滤字符串(html标签，表情，特殊字符)
//字符串，替换内容（special-特殊字符,html-html标签,emjoy-emjoy表情,word-小写字母，WORD-大写字母，number-数字,chinese-中文），要替换成什么，默认'',保留哪些特殊字符
//如果需要过滤多种字符，type参数使用,分割，如下栗子
//过滤字符串的html标签，大写字母，中文，特殊字符，全部替换成*,但是特殊字符'%'，'?'，除了这两个，其他特殊字符全部清除
//var str='asd    654a大蠢sasdasdASDQWEXZC6d5#%^*^&*^%^&*$\\"\'#@!()*/-())_\'":"{}?<div></div><img src=""/>啊实打实大蠢猪自行车这些课程';
// filterStr(str,'html,WORD,chinese,special','*','%?')
//result："asd    654a**sasdasd*********6d5#%^*^&*^%^&*$\"'#@!()*/-())_'":"{}?*****************"

filterStr: function (str, type, restr, spstr) {
    var typeArr = type.split(','), _str = str;
    for (var i = 0, len = typeArr.length; i < len; i++) {
        //是否是过滤特殊符号
        if (typeArr[i] === 'special') {
            var pattern, regText = '$()[]{}?\|^*+./\"\'+';
            //是否有哪些特殊符号需要保留
            if (spstr) {
                var _spstr = spstr.split(""), _regText = "[^0-9A-Za-z\\s";
                for (var j = 0, len1 = _spstr.length; j < len1; j++) {
                    if (regText.indexOf(_spstr[j]) === -1) {
                        _regText += _spstr[j];
                    }
                    else {
                        _regText += '\\' + _spstr[j];
                    }
                }
                _regText += ']'
                pattern = new RegExp(_regText, 'g');
            }
            else {
                pattern = new RegExp("[^0-9A-Za-z\\s]", 'g')
            }
        }
        var _restr = restr || '';
        switch (typeArr[i]) {
            case 'special':
                _str = _str.replace(pattern, _restr);
                break;
            case 'html':
                _str = _str.replace(/<\/?[^>]*>/g, _restr);
                break;
            case 'emjoy':
                _str = _str.replace(/[^\u4e00-\u9fa5|\u0000-\u00ff|\u3002|\uFF1F|\uFF01|\uff0c|\u3001|\uff1b|\uff1a|\u3008-\u300f|\u2018|\u2019|\u201c|\u201d|\uff08|\uff09|\u2014|\u2026|\u2013|\uff0e]/g, _restr);
                break;
            case 'word':
                _str = _str.replace(/[a-z]/g, _restr);
                break;
            case 'WORD':
                _str = _str.replace(/[A-Z]/g, _restr);
                break;
            case 'number':
                _str = _str.replace(/[0-9]/g, _restr);
                break;
            case 'chinese':
                _str = _str.replace(/[\u4E00-\u9FA5]/g, _restr);
                break;
        }
    }
    return _str;
}
 
```
### 2-11格式化处理字符串

```
//formatText('1234asda567asd890')
//result："12,34a,sda,567,asd,890"

//formatText('1234asda567asd890',4,' ')
//result："1 234a sda5 67as d890"

//formatText('1234asda567asd890',4,'-')
//result："1-234a-sda5-67as-d890"

formatText: function (str, size, delimiter) {
    var _size = size || 3, _delimiter = delimiter || ',';
    var regText = '\\B(?=(\\w{' + _size + '})+(?!\\w))';
    var reg = new RegExp(regText, 'g');
    return str.replace(reg, _delimiter);
}
 
```

### 2-12找出最长单词
```
//longestWord('Find the Longest word in a String')
//result：7

//longestWord('Find|the|Longest|word|in|a|String','|')
//result：7

longestWord: function (str, splitType) {
    var _splitType = splitType || /\s+/g,
        _max = 0,_item='';
    var strArr = str.split(_splitType);
    strArr.forEach(function (item) {
        if (_max < item.length) {
            _max = item.length
            _item=item;
        }
    })
    return {el:_item,max:_max};
}
 
```
### 2-13现金额转大写
```
/**
 * 
 * @desc   现金额转大写
 * @param  {Number} n 
 * @return {String}
 */
function digitUppercase(n) {
    var fraction = ['角', '分'];
    var digit = [
        '零', '壹', '贰', '叁', '肆',
        '伍', '陆', '柒', '捌', '玖'
    ];
    var unit = [
        ['元', '万', '亿'],
        ['', '拾', '佰', '仟']
    ];
    var head = n < 0 ? '欠' : '';
    n = Math.abs(n);
    var s = '';
    for (var i = 0; i < fraction.length; i++) {
        s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, '');
    }
    s = s || '整';
    n = Math.floor(n);
    for (var i = 0; i < unit[0].length && n > 0; i++) {
        var p = '';
        for (var j = 0; j < unit[1].length && n > 0; j++) {
            p = digit[n % 10] + unit[1][j] + p;
            n = Math.floor(n / 10);
        }
        s = p.replace(/(零.)*零$/, '').replace(/^$/, '零') + unit[0][i] + s;
    }
    return head + s.replace(/(零.)*零元/, '元')
        .replace(/(零.)+/g, '零')
        .replace(/^整$/, '零元整');
};
```

## 3.数组操作

### 3-1数组去重
```
removeRepeatArray: function (arr) {
    return arr.filter(function (item, index, self) {
        return self.indexOf(item) === index;
    });
}
 
```
### 3-2数组顺序打乱
```
upsetArr: function (arr) {
    return arr.sort(function () {
        return Math.random() - 0.5
    });
},
```
### 3-3数组最大值最小值
```
//数组最大值
maxArr: function (arr) {
    return Math.max.apply(null, arr);
},
//数组最小值
minArr: function (arr) {
    return Math.min.apply(null, arr);
}
 
```

### 3-4数组求和，平均值
```
//这一块的封装，主要是针对数字类型的数组
//求和
sumArr: function (arr) {
    return arr.reduce(function (pre, cur) {
        return pre + cur
    })
}
//数组平均值,小数点可能会有很多位，这里不做处理，处理了使用就不灵活！
covArr: function (arr) {
    return this.sumArr(arr) / arr.length;
},
 
```

###3-5从数组中随机获取元素
```
//randomOne([1,2,3,6,8,5,4,2,6])
//2
//randomOne([1,2,3,6,8,5,4,2,6])
//8
//randomOne([1,2,3,6,8,5,4,2,6])
//8
//randomOne([1,2,3,6,8,5,4,2,6])
//1

randomOne: function (arr) {
    return arr[Math.floor(Math.random() * arr.length)];
}
 
```
### 3-6回数组字符串一个元素出现的次数
```
//getEleCount('asd56+asdasdwqe','a')
//result：3
//getEleCount([1,2,3,4,5,66,77,22,55,22],22)
//result：2

getEleCount: function (obj, ele) {
    var num = 0;
    for (var i = 0, len = obj.length; i < len; i++) {
        if (ele === obj[i]) {
            num++;
        }
    }
    return num;
}

```

### 3-7数组/字符串出现最多的几次元素和出现次数
```
//arr, rank->长度，默认为数组长度，ranktype，排序方式，默认降序
//返回值：el->元素，count->次数
//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2])
//默认情况，返回所有元素出现的次数
//result：[{"el":"2","count":6},{"el":"1","count":4},{"el":"3","count":2},{"el":"4","count":1},{"el":"5","count":1},{"el":"6","count":1}]

//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],3)
//传参（rank=3），只返回出现次数排序前三的
//result：[{"el":"2","count":6},{"el":"1","count":4},{"el":"3","count":2}]

//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],null,1)
//传参（ranktype=1,rank=null），升序返回所有元素出现次数
//result：[{"el":"6","count":1},{"el":"5","count":1},{"el":"4","count":1},{"el":"3","count":2},{"el":"1","count":4},{"el":"2","count":6}]

//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],3,1)
//传参（rank=3，ranktype=1），只返回出现次数排序（升序）前三的
//result：[{"el":"6","count":1},{"el":"5","count":1},{"el":"4","count":1}]

getCount: function (arr, rank, ranktype) {
    var obj = {},
        k, arr1 = []
    //记录每一元素出现的次数
    for (var i = 0, len = arr.length; i < len; i++) {
        k = arr[i];
        if (obj[k]) {
            obj[k]++;
        } else {
            obj[k] = 1;
        }
    }
    //保存结果{el-'元素'，count-出现次数}
    for (var o in obj) {
        arr1.push({el: o, count: obj[o]});
    }
    //排序（降序）
    arr1.sort(function (n1, n2) {
        return n2.count - n1.count
    });
    //如果ranktype为1，则为升序，反转数组
    if (ranktype === 1) {
        arr1 = arr1.reverse();
    }
    var rank1 = rank || arr1.length;
    return arr1.slice(0, rank1);
}
 
```
###3-8得到n1-n2下标的数组
```
//getArrayNum([0,1,2,3,4,5,6,7,8,9],5,9)
//result：[5, 6, 7, 8, 9]

//getArrayNum([0,1,2,3,4,5,6,7,8,9],2) //不传第二个参数,默认返回从n1到数组结束的元素
//result：[2, 3, 4, 5, 6, 7, 8, 9]

getArrayNum: function (arr, n1, n2) {
    return arr.slice(n1, n2);
}
 
```
### 3-9筛选数组

```
//删除值为'val'的数组元素
//removeArrayForValue(['test','test1','test2','test','aaa'],'test',')
//result：["aaa"]   带有'test'的都删除

//removeArrayForValue(['test','test1','test2','test','aaa'],'test')
//result：["test1", "test2", "aaa"]  //数组元素的值全等于'test'才被删除

removeArrayForValue: function (arr, val, type) {
    return arr.filter(function (item) {
        return type ? item.indexOf(val) === -1 : item !== val
    })
}
 
```
### 3-10 获取对象数组某些项
```
//var arr=[{a:1,b:2,c:9},{a:2,b:3,c:5},{a:5,b:9},{a:4,b:2,c:5},{a:4,b:5,c:7}]
//getOptionArray(arr,'a,c')
//result：[{a:1,c:9},{a:2,c:5},{a:5,c:underfind},{a:4,c:5},{a:4,c:7}]

//getOptionArray(arr,'b')
//result：[2, 3, 9, 2, 5]

getOptionArray: function (arr, keys) {
    var newArr = []
    if (!keys) {
        return arr
    }
    var _keys = keys.split(','), newArrOne = {};
    //是否只是需要获取某一项的值
    if (_keys.length === 1) {
        for (var i = 0, len = arr.length; i < len; i++) {
            newArr.push(arr[i][keys])
        }
        return newArr;
    }
    for (var i = 0, len = arr.length; i < len; i++) {
        newArrOne = {};
        for (var j = 0, len1 = _keys.length; j < len1; j++) {
            newArrOne[_keys[j]] = arr[i][_keys[j]]
        }
        newArr.push(newArrOne);
    }
    return newArr
}
 
```

### 3-11 排除对象数组某些项 

```
//var arr=[{a:1,b:2,c:9},{a:2,b:3,c:5},{a:5,b:9},{a:4,b:2,c:5},{a:4,b:5,c:7}]
//filterOptionArray(arr,'a')
//result：[{b:2,c:9},{b:3,c:5},{b:9},{b:2,c:5},{b:5,c:7}]
//filterOptionArray(arr,'a,c')
//result：[{b:2},{b:3},{b:9},{b:2},{b:5}]
filterOptionArray: function (arr, keys) {
    var newArr = []
    var _keys = keys.split(','), newArrOne = {};
    for (var i = 0, len = arr.length; i < len; i++) {
        newArrOne = {};
        for (var key in arr[i]) {
            //如果key不存在排除keys里面,添加数据
            if (_keys.indexOf(key) === -1) {
                newArrOne[key] = arr[i][key];
            }
        }
        newArr.push(newArrOne);
    }
    return newArr
}
 
```

### 3-12 对象数组排序

```
//var arr=[{a:1,b:2,c:9},{a:2,b:3,c:5},{a:5,b:9},{a:4,b:2,c:5},{a:4,b:5,c:7}]
//arraySort(arr,'a,b')a是第一排序条件，b是第二排序条件
//result：[{"a":1,"b":2,"c":9},{"a":2,"b":3,"c":5},{"a":4,"b":2,"c":5},{"a":4,"b":5,"c":7},{"a":5,"b":9}]

arraySort: function (arr, sortText) {
    if (!sortText) {
        return arr
    }
    var _sortText = sortText.split(',').reverse(), _arr = arr.slice(0);
    for (var i = 0, len = _sortText.length; i < len; i++) {
        _arr.sort(function (n1, n2) {
            return n1[_sortText[i]] - n2[_sortText[i]]
        })
    }
    return _arr;
}
 
```
### 3-13 判断两个数组是否相等
```
/**
 * 
 * @desc 判断两个数组是否相等
 * @param {Array} arr1 
 * @param {Array} arr2 
 * @return {Boolean}
 */
function arrayEqual(arr1, arr2) {
    if (arr1 === arr2) return true;
    if (arr1.length != arr2.length) return false;
    for (var i = 0; i < arr1.length; ++i) {
        if (arr1[i] !== arr2[i]) return false;
    }
    return true;
}
```

## 4.基础DOM操作

### 4-1检测对象是否有哪个类名
```
//方法一
//检测对象是否有哪个类名
hasClass: function (obj, classStr) {
    if (obj.className && this.trim(obj.className, 1) !== "") {
        var arr = obj.className.split(/\s+/); //这个正则表达式是因为class可以有多个,判断是否包含
        return (arr.indexOf(classStr) == -1) ? false : true;
    }
    else {
        return false;
    }
}

//方法二
/**
 * 
 * @desc 判断元素是否有某个class
 * @param {HTMLElement} ele 
 * @param {String} cls 
 * @return {Boolean}
 */
function hasClass(ele, cls) {
    return (new RegExp('(\\s|^)' + cls + '(\\s|$)')).test(ele.className);
}
 
```
### 4-2 添加类名

```
addClass: function (obj, classStr) {
    if ((this.istype(obj, 'array') || this.istype(obj, 'elements')) && obj.length >= 1) {
        for (var i = 0, len = obj.length; i < len; i++) {
            if (!this.hasClass(obj[i], classStr)) {
                obj[i].className += " " + classStr;
            }
        }
    }
    else {
        if (!this.hasClass(obj, classStr)) {
            obj.className += " " + classStr;
        }
    }
}
 
```
### 4-3删除类名
```
removeClass: function (obj, classStr) {
    if ((this.istype(obj, 'array') || this.istype(obj, 'elements')) && obj.length > 1) {
        for (var i = 0, len = obj.length; i < len; i++) {
            if (this.hasClass(obj[i], classStr)) {
                var reg = new RegExp('(\\s|^)' + classStr + '(\\s|$)');
                obj[i].className = obj[i].className.replace(reg, '');
            }
        }
    }
    else {
        if (this.hasClass(obj, classStr)) {
            var reg = new RegExp('(\\s|^)' + classStr + '(\\s|$)');
            obj.className = obj.className.replace(reg, '');
        }
    }
}
 
```
###4-4替换类名("被替换的类名","替换的类名")
```
replaceClass: function (obj, newName, oldName) {
    this.removeClass(obj, oldName);
    this.addClass(obj, newName);
}
```
### 4-5设置样式
```
css: function (obj, json) {
    for (var attr in json) {
        obj.style[attr] = json[attr];
    }
}
```
### 4-6设置文本内容
```
//设置对象内容
// html(document.getElementById('xxx'),'hello world')

html: function (obj) {
    if (arguments.length === 1) {
        return obj.innerHTML;
    } else if (arguments.length === 2) {
        obj.innerHTML = arguments[1];
    }
}
text: function (obj) {
    if (arguments.length === 1) {
        return obj.innerHTML;
    } else if (arguments.length === 2) {
        obj.innerHTML = this.filterStr(arguments[1],'html');
    }
}
 
```
### 4-7显示隐藏
```
show: function (obj) {
    var blockArr=['div','li','ul','ol','dl','table','article','h1','h2','h3','h4','h5','h6','p','hr','header','footer','details','summary','section','aside','']
    if(blockArr.indexOf(obj.tagName.toLocaleLowerCase())===-1){
        obj.style.display ='inline';
    }
    else{
        obj.style.display ='block';
    }
},
hide: function (obj) {
    obj.style.display = "none";
}
 
```
###  4-8获取滚动条距顶部的距离
```
/**
 * 
 * @desc 获取滚动条距顶部的距离
 */
function getScrollTop() {
    return (document.documentElement && document.documentElement.scrollTop) || document.body.scrollTop;
}
``` 
###  4-9获取元素的距离文档的位置
```
/**
 * 
 * @desc  获取一个元素的距离文档(document)的位置，类似jQ中的offset()
 * @param {HTMLElement} ele 
 * @returns { {left: number, top: number} }
 */
function offset(ele) {
    var pos = {
        left: 0,
        top: 0
    };
    while (ele) {
        pos.left += ele.offsetLeft;
        pos.top += ele.offsetTop;
        ele = ele.offsetParent;
    };
    return pos;
}
``` 
###  5-0获取元素的距离文档的位置
```
/**
 * 
 * @desc 设置滚动条距顶部的距离
 */
function setScrollTop(value) {
    window.scrollTo(0, value);
    return value;
}
```
### 5.1 滚动条平滑滚动指定位置
```
var getScrollTop = require('./getScrollTop');
var setScrollTop = require('./setScrollTop');
var requestAnimFrame = (function () {
    return window.requestAnimationFrame ||
        window.webkitRequestAnimationFrame ||
        window.mozRequestAnimationFrame ||
        function (callback) {
            window.setTimeout(callback, 1000 / 60);
        };
})();
/**
 * 
 * @desc  在${duration}时间内，滚动条平滑滚动到${to}指定位置
 * @param {Number} to 
 * @param {Number} duration 
 */
function scrollTo(to, duration) {
    if (duration < 0) {
        setScrollTop(to);
        return
    }
    var diff = to - getScrollTop();
    if (diff === 0) return
    var step = diff / duration * 10;
    requestAnimationFrame(
        function () {
            if (Math.abs(step) > Math.abs(diff)) {
                setScrollTop(getScrollTop() + diff);
                return;
            }
            setScrollTop(getScrollTop() + step);
            if (diff > 0 && getScrollTop() >= to || diff < 0 && getScrollTop() <= to) {
                return;
            }
            scrollTo(to, duration - 16);
        });
}
```
## 5 Random 随机值

### 5-1 随机生成颜色
```
/**
 * 
 * @desc 随机生成颜色
 * @return {String} 
 */
function randomColor() {
    return '#' + ('00000' + (Math.random() * 0x1000000 << 0).toString(16)).slice(-6);
}
```
### 5-2 生成指定范围随机数
```
/**
 * 
 * @desc 生成指定范围随机数
 * @param  {Number} min 
 * @param  {Number} max 
 * @return {Number} 
 */
function randomNum(min, max) {
    return Math.floor(min + Math.random() * (max - min));
}
```

## 6 获取，设置url参数

### 6-1 url参数转对象
```
/**
 * 
 * @desc   url参数转对象
 * @param  {String} url  default: window.location.href
 * @return {Object} 
 */
 
function parseQueryString(url) {
    url = url == null ? window.location.href : url
    var search = url.substring(url.lastIndexOf('?') + 1)
    if (!search) {
        return {}
    }
    return JSON.parse('{"' + decodeURIComponent(search).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g, '":"') + '"}')
}
```
### 6-2 设置url参数
```
//设置url参数
//setUrlPrmt({'a':1,'b':2})
//result：a=1&b=2

setUrlPrmt: function (obj) {
    var _rs = [];
    for (var p in obj) {
        if (obj[p] != null && obj[p] != '') {
            _rs.push(p + '=' + obj[p])
        }
    }
    return _rs.join('&');
}
```
### 6-3 获取url参数
```
//getUrlPrmt('test.com/write?draftId=122000011938')
//result：Object{draftId: "122000011938"}

getUrlPrmt: function (url) {
    url = url ? url : window.location.href;
    var _pa = url.substring(url.indexOf('?') + 1),
        _arrS = _pa.split('&'),
        _rs = {};
    for (var i = 0, _len = _arrS.length; i < _len; i++) {
        var pos = _arrS[i].indexOf('=');
        if (pos == -1) {
            continue;
        }
        var name = _arrS[i].substring(0, pos),
            value = window.decodeURIComponent(_arrS[i].substring(pos + 1));
        _rs[name] = value;
    }
    return _rs;
}
 
```
### 获取指定url参数
```
function GetQueryString(name) {
	var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
	var r = window.location.search.substr(1).match(reg);
	if(r != null) {
		return unescape(r[2]);
	}
	return null;
}
var redirectUrl = GetQueryString('r')
```

## 7 Time 时间

### 7-1 到某一个时间的倒计时
```
//到某一个时间的倒计时
//getEndTime('2017/7/22 16:0:0')
//result："剩余时间6天 2小时 28 分钟20 秒"

getEndTime: function (endTime) {
    var startDate = new Date(); //开始时间，当前时间
    var endDate = new Date(endTime); //结束时间，需传入时间参数
    var t = endDate.getTime() - startDate.getTime(); //时间差的毫秒数
    var d = 0,
        h = 0,
        m = 0,
        s = 0;
    if (t >= 0) {
        d = Math.floor(t / 1000 / 3600 / 24);
        h = Math.floor(t / 1000 / 60 / 60 % 24);
        m = Math.floor(t / 1000 / 60 % 60);
        s = Math.floor(t / 1000 % 60);
    }
    return "剩余时间" + d + "天 " + h + "小时 " + m + " 分钟" + s + " 秒";
}
 
```
### 7-2 时间戳转日期
```
// 时间戳转日期格式
	function timestampToTime(timestamp) {
		var date = new Date(timestamp); //时间戳为10位需*1000，时间戳为13位的话不需乘1000
		Y = date.getFullYear() + '-';
		M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
		D = date.getDate() + ' ';
		return Y + M + D;
	}
```
## 8 封装ajax函数
```
/*
 * url				地址
 * method			请求方式get/post
 * dataType			返回什么数据类型srging/json/xml
 * data				请求时候的传的数据（它是一个对象）
 * succ				成功后的回调函数
 * fail				失败后的回调函数
 * 
 */

/*
	ajax({
		url: 'php/get_json.php',
		method: 'get',
		dataType: 'json',
		data: {
			'user': encodeURI(inputs[0].value),
			'password': inputs[1].value,
			'email': inputs[2].value
		},
		succ: function(data) {
			console.log(data);
		},
		fail: function(data) {
			alert(data);
		}
	});
		
*/

function ajax(json) {
	var settings = {
		url: '',
		method: 'get',
		data: {},
		dataType: 'json',
		succ: function() {},
		fail: function() {}
	};

	//用户传的参数覆盖默认参数
	for(var attr in json) {
		settings[attr] = json[attr];
	}

	//把数据拼成正确的格式
	var arr = [];
	for(var attr in settings.data) {
		arr.push(attr + '=' + settings.data[attr]);
	}
	settings.data = arr.join('&');

	//声明一个ajax对象
	var ajax = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP');

	//设置请求方式
	if(settings.method.toLocaleLowerCase() === 'get') {
		ajax.open(settings.method, settings.url + '?' + settings.data + '&' + new Date().getTime(), true);
		ajax.send();
	} else {
		ajax.open(settings.method, settings.url, true);
		ajax.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
		ajax.send(settings.data);
	}

	//设置完成事件的兼容性
	if(typeof ajax.onload === 'undefined') {
		ajax.onreadystatechange = ready;
	} else {
		ajax.onload = ready;
	}

	function ready() {
		if(ajax.readyState == 4) {
			if(ajax.status == 200) {
				switch(settings.dataType.toLocaleLowerCase()) {
					case 'string':
						settings.succ(ajax.responseText);
						break;

					case 'json':
						settings.succ(JSON.parse(ajax.responseText));
						break;

					case 'xml':
						settings.succ(ajax.responseXML);
				}
			} else {
				settings.fail(ajax.status);
			}
		}
	};
}
```

## 9 图片懒加载

```
//图片没加载出来时用一张图片代替
aftLoadImg: function (obj, url, errorUrl,cb) {
    var oImg = new Image(), _this = this;
    oImg.src = url;
    oImg.onload = function () {
        obj.src = oImg.src;
        if (cb && _this.istype(cb, 'function')) {
            cb(obj);
        }
    }
    oImg.onerror=function () {
        obj.src=errorUrl;
        if (cb && _this.istype(cb, 'function')) {
            cb(obj);
        }
    }
},
//图片滚动懒加载
//@className {string} 要遍历图片的类名
//@num {number} 距离多少的时候开始加载 默认 0
//比如，一张图片距离文档顶部3000，num参数设置200，那么在页面滚动到2800的时候，图片加载。不传num参数就滚动，num默认是0，页面滚动到3000就加载
//html代码
//<p><img data-src="https://user-gold-cdn.xitu.io/2017/12/7/160319f12631736f" class="load-img" width='528' height='304' /></p>
//<p><img data-src="https://user-gold-cdn.xitu.io/2017/12/7/160319f12631736f" class="load-img" width='528' height='304' /></p>
//<p><img data-src="https://user-gold-cdn.xitu.io/2017/12/7/160319f12631736f" class="load-img" width='528' height='304' /></p>....
//data-src储存src的数据，到需要加载的时候把data-src的值赋值给src属性，图片就会加载。
//详细可以查看testLoadImg.html
//window.onload = function() {
//    loadImg('load-img',100);
//    window.onscroll = function() {
//        loadImg('load-img',100);
//        }
//}
loadImg: function (className, num, errorUrl) {
    var _className = className || 'ec-load-img', _num = num || 0, _this = this,_errorUrl=errorUrl||null;
    var oImgLoad = document.getElementsByClassName(_className);
    for (var i = 0, len = oImgLoad.length; i < len; i++) {
        //如果图片已经滚动到指定的高度
        if (document.documentElement.clientHeight + document.documentElement.scrollTop > oImgLoad[i].offsetTop - _num && !oImgLoad[i].isLoad) {
            //记录图片是否已经加载
            oImgLoad[i].isLoad = true;
            //设置过渡，当图片下来的时候有一个图片透明度变化
            oImgLoad[i].style.cssText = "transition: ''; opacity: 0;"
            if (oImgLoad[i].dataset) {
                this.aftLoadImg(oImgLoad[i], oImgLoad[i].dataset.src, _errorUrl, function (o) {
                    //添加定时器，确保图片已经加载完了，再把图片指定的的class，清掉，避免重复编辑
                    setTimeout(function () {
                        if (o.isLoad) {
                            _this.removeClass(o, _className);
                            o.style.cssText = "";
                        }
                    }, 1000)
                });
            } else {
                this.aftLoadImg(oImgLoad[i], oImgLoad[i].getAttribute("data-src"), _errorUrl, function (o) {
                    //添加定时器，确保图片已经加载完了，再把图片指定的的class，清掉，避免重复编辑
                    setTimeout(function () {
                        if (o.isLoad) {
                            _this.removeClass(o, _className);
                            o.style.cssText = "";
                        }
                    }, 1000)
                });
            }
            (function (i) {
                setTimeout(function () {
                    oImgLoad[i].style.cssText = "transition:all 1s; opacity: 1;";
                }, 16)
            })(i);
        }
    }
}
 
```

## 10 关键词加标签/高亮

```
//这两个函数多用于搜索的时候，关键词高亮
//创建正则字符
//createKeyExp([前端，过来])
//result:(前端|过来)/g

createKeyExp: function (strArr) {
    var str = "";
    for (var i = 0; i < strArr.length; i++) {
        if (i != strArr.length - 1) {
            str = str + strArr[i] + "|";
        } else {
            str = str + strArr[i];
        }
    }
    return "(" + str + ")";
}

//关键字加标签（多个关键词用空格隔开）
//findKey('守侯我oaks接到了来自下次你离开快乐吉祥留在开城侯','守侯 开','i')
//"<i>守侯</i>我oaks接到了来自下次你离<i>开</i>快乐吉祥留在<i>开</i>城侯"

findKey: function (str, key, el) {
    var arr = null,
        regStr = null,
        content = null,
        Reg = null,
        _el = el || 'span';
    arr = key.split(/\s+/);
    //alert(regStr); //    如：(前端|过来)
    regStr = this.createKeyExp(arr);
    content = str;
    //alert(Reg);//        /如：(前端|过来)/g
    Reg = new RegExp(regStr, "g");
    //过滤html标签 替换标签，往关键字前后加上标签
    content = content.replace(/<\/?[^>]*>/g, '')
    return content.replace(Reg, "<" + _el + ">$1</" + _el + ">");
}
 
```
## 11 数据类型判断 
```
//istype([],'array')
//true
//istype([])
//'[object Array]'
istype: function (o, type) {
    if (type) {
        var _type = type.toLowerCase();
    }
    switch (_type) {
        case 'string':
            return Object.prototype.toString.call(o) === '[object String]';
        case 'number':
            return Object.prototype.toString.call(o) === '[object Number]';
        case 'boolean':
            return Object.prototype.toString.call(o) === '[object Boolean]';
        case 'undefined':
            return Object.prototype.toString.call(o) === '[object Undefined]';
        case 'null':
            return Object.prototype.toString.call(o) === '[object Null]';
        case 'function':
            return Object.prototype.toString.call(o) === '[object Function]';
        case 'array':
            return Object.prototype.toString.call(o) === '[object Array]';
        case 'object':
            return Object.prototype.toString.call(o) === '[object Object]';
        case 'nan':
            return isNaN(o);
        case 'elements':
            return Object.prototype.toString.call(o).indexOf('HTML') !== -1
        default:
            return Object.prototype.toString.call(o)
    }
}
 
```
## 12 手机类型判断
```
browserInfo: function (type) {
    switch (type) {
        case 'android':
            return navigator.userAgent.toLowerCase().indexOf('android') !== -1
        case 'iphone':
            return navigator.userAgent.toLowerCase().indexOf('iphone') !== -1
        case 'ipad':
            return navigator.userAgent.toLowerCase().indexOf('ipad') !== -1
        case 'weixin':
            return navigator.userAgent.toLowerCase().indexOf('micromessenger') !== -1
        default:
            return navigator.userAgent.toLowerCase()
    }
}
 
```
## 13 函数节流
```
//多用于鼠标滚动，移动，窗口大小改变等高频率触发事件
// var count=0;
// function fn1(){
//     count++;
//     console.log(count)
// }
// //100ms内连续触发的调用，后一个调用会把前一个调用的等待处理掉，但每隔200ms至少执行一次
// document.onmousemove=delayFn(fn1,100,200)

delayFn: function (fn, delay, mustDelay) {
    var timer = null;
    var t_start;
    return function () {
        var context = this, args = arguments, t_cur = +new Date();
        //先清理上一次的调用触发（上一次调用触发事件不执行）
        clearTimeout(timer);
        //如果不存触发时间，那么当前的时间就是触发时间
        if (!t_start) {
            t_start = t_cur;
        }
        //如果当前时间-触发时间大于最大的间隔时间（mustDelay），触发一次函数运行函数
        if (t_cur - t_start >= mustDelay) {
            fn.apply(context, args);
            t_start = t_cur;
        }
        //否则延迟执行
        else {
            timer = setTimeout(function () {
                fn.apply(context, args);
            }, delay);
        }
    };
}
 
```

## 14 常用正则
```
/ 常见的 正则表达式 校验
// QQ号、手机号、Email、是否是数字、去掉前后空格、是否存在中文、邮编、身份证、URL、日期格式、IP
var myRegExp = {
    // 检查字符串是否为合法QQ号码
    isQQ: function(str) {
        // 1 首位不能是0  ^[1-9]
        // 2 必须是 [5, 11] 位的数字  \d{4, 9}
        var reg = /^[1-9][0-9]{4,9}$/gim;
        if (reg.test(str)) {
            console.log('QQ号码格式输入正确');
            return true;
        } else {
            console.log('请输入正确格式的QQ号码');
            return false;
        }
    },
    // 检查字符串是否为合法手机号码
    isPhone: function(str) {
        var reg = /^(0|86|17951)?(13[0-9]|15[012356789]|18[0-9]|14[57]|17[678])[0-9]{8}$/;
        if (reg.test(str)) {
            console.log('手机号码格式输入正确');
            return true;
        } else {
            console.log('请输入正确格式的手机号码');
            return false;
        }
    },
    // 检查字符串是否为合法Email地址
    isEmail: function(str) {
        var reg = /^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/;
        // var reg = /\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*/;
        if (reg.test(str)) {
            console.log('Email格式输入正确');
            return true;
        } else {
            console.log('请输入正确格式的Email');
            return false;
        }
    },
    // 检查字符串是否是数字
    isNumber: function(str) {
        var reg = /^\d+$/;
        if (reg.test(str)) {
            console.log(str + '是数字');
            return true;
        } else {
            console.log(str + '不是数字');
            return false;
        }
    },
    // 去掉前后空格
    trim: function(str) {
        var reg = /^\s+|\s+$/g;
        return str.replace(reg, '');
    },
    // 检查字符串是否存在中文
    isChinese: function(str) {
        var reg = /[\u4e00-\u9fa5]/gm;
        if (reg.test(str)) {
            console.log(str + ' 中存在中文');
            return true;
        } else {
            console.log(str + ' 中不存在中文');
            return false;
        }
    },
    // 检查字符串是否为合法邮政编码
    isPostcode: function(str) {
        // 起始数字不能为0，然后是5个数字  [1-9]\d{5}
        var reg = /^[1-9]\d{5}$/g;
        // var reg = /^[1-9]\d{5}(?!\d)$/;
        if (reg.test(str)) {
            console.log(str + ' 是合法的邮编格式');
            return true;
        } else {
            console.log(str + ' 是不合法的邮编格式');
            return false;
        }
    },
    // 检查字符串是否为合法身份证号码
    isIDcard: function(str) {
        var reg = /^(^[1-9]\d{7}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}$)|(^[1-9]\d{5}[1-9]\d{3}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])((\d{4})|\d{3}[Xx])$)$/;
        if (reg.test(str)) {
            console.log(str + ' 是合法的身份证号码');
            return true;
        } else {
            console.log(str + ' 是不合法的身份证号码');
            return false;
        }
    },
    // 检查字符串是否为合法URL
    isURL: function(str) {
        var reg = /^https?:\/\/(([a-zA-Z0-9_-])+(\.)?)*(:\d+)?(\/((\.)?(\?)?=?&?[a-zA-Z0-9_-](\?)?)*)*$/i;
        if (reg.test(str)) {
            console.log(str + ' 是合法的URL');
            return true;
        } else {
            console.log(str + ' 是不合法的URL');
            return false;
        }
    },
    // 检查字符串是否为合法日期格式 yyyy-mm-dd
    isDate: function(str) {
        var reg = /^[1-2][0-9][0-9][0-9]-[0-1]{0,1}[0-9]-[0-3]{0,1}[0-9]$/;
        if (reg.test(str)) {
            console.log(str + ' 是合法的日期格式');
            return true;
        } else {
            console.log(str + ' 是不合法的日期格式，yyyy-mm-dd');
            return false;
        }
    },
    // 检查字符串是否为合法IP地址
    isIP: function(str) {
        // 1.1.1.1  四段  [0 , 255]
        // 第一段不能为0
        // 每个段不能以0开头
        //
        // 本机IP: 58.50.120.18 湖北省荆州市 电信
        var reg = /^([1-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])(\.([0-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])){3}$/gi;
        if (reg.test(str)) {
            console.log(str + ' 是合法的IP地址');
            return true;
        } else {
            console.log(str + ' 是不合法的IP地址');
            return false;
        }
    }
}
// 测试
// console.log(myRegExp.isQQ('80583600'));
// console.log(myRegExp.isPhone('17607160722'));
// console.log(myRegExp.isEmail('80583600@qq.com'));
// console.log(myRegExp.isNumber('100a'));
// console.log(myRegExp.trim('  100  '));
// console.log(myRegExp.isChinese('baixiaoming'));
// console.log(myRegExp.isChinese('小明'));
// console.log(myRegExp.isPostcode('412345'));
// console.log(myRegExp.isIDcard('42091119940927001X'));
// console.log(myRegExp.isURL('https://www.baidu.com/'));
// console.log(myRegExp.isDate('2017-4-4'));
// console.log(myRegExp.isIP('1.0.0.0'));
```
## 15 其他拓展-不断添加
### 15-1 多张无缝轮播
```
<html>
<head>
	<title></title>
	<meta charset="UTF-8" />
</head>
<style>
	* {
		margin: 0;
		padding: 0;
	}
	
	#div1 {
		width: 800px;
		height: 130px;
		margin: 100px auto;
		position: relative;
		overflow: hidden;
	}
	
	#div1 ul {
		position: absolute;
		left: 0;
		top: 0;
	}
	
	#div1 ul li {
		font: 30px/130px "微软雅黑";
		text-align: center;
		float: left;
		list-style: none;
		width: 200px;
		height: 130px;
		background: yellowgreen;
		border: 1px solid seagreen;
		box-sizing: border-box;
	}
</style>
<body>

	<div id="div1">
		<ul>
			<li>1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
		</ul>
	</div>
</body>
<script>
	window.onload = function() {
		slider('div1')
		function slider(obj) {
			var oDiv = document.getElementById(obj);
			var oUl = oDiv.getElementsByTagName("ul")[0];
			var oLi = oDiv.getElementsByTagName("li");

			oUl.innerHTML = oUl.innerHTML + oUl.innerHTML;

			oUl.style.width = oLi[0].offsetWidth * oLi.length + "px";

			//移动速度
			var speed = 1;

			//鼠标移开  
			function move() {
				if(oUl.offsetLeft < -oUl.offsetWidth / 2) {
					oUl.style.left = "0";
				}

				if(oUl.offsetLeft > 0) {
					oUl.style.left = -oUl.offsetWidth / 2 + "px";
				}

				oUl.style.left = oUl.offsetLeft - speed + "px";

			}

			//定时器  控制移动的时间
			var timer = setInterval(move, 16);

			//鼠标移入
			oDiv.onmouseover = function() {
				clearInterval(timer);
			}

			//鼠标移开
			oDiv.onmouseout = function() {
				timer = setInterval(move, 16);
			}
		}

	}
</script>
</html>
```

