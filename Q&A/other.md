#### 统计字符串中字符出现的次数
```
function count(str) {
        const arr = str.split('')
        const result = {}
        for(let i of arr){
            if (!result[i]){
                result[i] = 1
            }else {
                result[i]++
            }
        }
        for(let k in result){
            console.log(`${k}:${result[k]}`)
        }
    }
    count('javascript')
```
用正则匹配指定字符串出现次数
```
return str.match(reg).length
```
