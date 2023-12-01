<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-12-01 16:15:20
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-12-01 16:49:55
 * @FilePath: \question-Interview\highFrequent\002-js-unique\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{数组去重}$

### 去重方式
###### (不考虑传入参数不是数组的情况，需要的话自行判断)
1. $\color{#00a361}{new \ Set}$
```
var unique = function (arr) {
  return Array.from(new Set(arr));
};

let res = unique([2,3,4,4,5,5,5,6,6]);
console.log(res); //  [2, 3, 4, 5, 6]
```

2. $\color{#00a361}{for \ + \ includes }$
```
var unique = function (arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    if(!newArr.includes(arr[i])) {
      newArr.push(arr[i])
    }
  }
  return newArr;
};
```

3. $\color{#00a361}{for \ + \ indexOf }$
```
var unique = function (arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    if(newArr.indexOf(arr[i]) == -1) {
      newArr.push(arr[i])
    }
  }
  return newArr;
};
```

4. $\color{#00a361}{filter去重}$
```
var unique = function (arr) {
  return arr.filter((item, index) => {
    return arr.indexOf(item) === index
  });
};
```

5. $\color{#00a361}{reduce去重}$
```
var unique = function (arr) {
  return arr.reduce((prev,cur) => {
    !prev.includes(cur) && prev.push(cur);
    return prev;
  }, [])
};
```

6. $\color{#00a361}{相邻元素去重}$
```
var unique = function (arr) {
  let newArr = [];
  arr.sort((a,b) => a - b);
  for (let i = 0, len = arr.length; i < len; i++) {
    if(arr[i] !== arr[i - 1]) {
      newArr.push(arr[i])
    }
  }
  return newArr;
};
```