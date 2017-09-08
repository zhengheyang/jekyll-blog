### 题目描述 
求一个字符串的最大回文前缀长度。回文是指正反方向读起来都一样的字符串，比如“abcdcba”就是一个回文。回文放在一个字符串的最前方就是回文前缀。求最大回文前缀的长度。

样例输入  sogou 样例输出 1

样例输入  abba 样例输出 4

样例输入  abcba 样例输出 5

样例输入  abcbaxiojhioahsfd 样例输出 5

* * *

### 首先分析题目：

1.什么是回文？简单的说，即无论正反排列内容完全相同；

2.什么是回文前缀？ 即回文必须在整段字符串的最前面；

3.什么是回文长度？......就是回文的长度咯......


解题思路：
根据题目要求，先拿到最大回文前缀，然后求出其长度，具体思路如下：

+ 获取用户输入的内容并转为数组----

+ 在数组中从后往前寻找与首位相等的值，如相等（该首尾相等部分可理解为具有成为回文的前提条件），删除相等值后段无用部分----

+ 循环判断数组的第2、3、4......位是否与倒数2、3、4......位相等，如全部相等，则该数组就是回文，否则递归回第2步继续。

完整代码如下：

<pre><code>

function getArr() {                     
            //获取用户输入的内容，并转化为数组        
            var usrArr = document.getElementById("usrInput").value;
            var strArr = [];
            for (var i = 0; i < usrArr.length; i++) {
                strArr.push(usrArr.substr(i, 1));
            }
            return strArr;
        }


        function palindrome(array) {
            for (var i = array.length - 1; i >= 0; i--) {                  
                //从末位往前，始终与数组首位相比较
                if (array[0] == array[i]) {                                
                    //若某位与数组首位相等，则该区间段具备成为回文的首要条件
                    array.splice(i + 1, array.length - 1);                 
                    //截去数组后段无用部分
                    break;                                                 
                }
            }
            if (array.length > 1) {
                if (array.length % 2 == 0) {                               
                    //判断上一步得到的数组长度为偶数还是奇数，若为偶数
                    for (var j = 0; j < array.length / 2; j++) {           
                        //比较首位与末位（此步可改为从第二位开始比较，因为得到的即是首尾相等的数组，此处从首位开始是为了便于理解）、首位+1与末位-1......循环次数为数组长度的1/2
                        if (array[j] == array[array.length - 1 - j]) {
                            continue;                                      
                            //如果相等，则继续下一次比较
                        } else {
                            array.pop();                                   
                            //如不等，说明前面拿到的具备成为回文首要条件的数组并不具备其他必要条件，删除数组末位
                            return palindrome(array);                      
                            //递归再次寻找
                        }
                    }
                } else {
                    for (var j = 0; j < (array.length - 1) / 2; j++) {     
                        //数组长度为奇数的情况，遍历次数为数组长度-1的一半，其余同上
                        if (array[j] == array[array.length - 1 - j]) {
                            continue;
                        } else {
                            array.pop();
                            return palindrome(array);
                        }
                    }
                }
            }
            var rs = array.length;                                          
             //得到回文数组的长度
            document.getElementById("rs").value = rs;
        }

</code></pre>