# resolve/join

resolve类似对路径逐一cd操作，而join而是路径的连接。

``` js
const path = require('path');
let myPath1 = path.join(__dirname,'/img/so', './about');
let myPath2 = path.join(__dirname,'./img/so', '/about');
let myPath3 = path.resolve(__dirname,'/img/so', './about');
let myPath4 = path.resolve(__dirname,'./img/so', '/about');
console.log(__dirname);        
console.log(myPath1); 
console.log(myPath2);   
console.log(myPath3); 
console.log(myPath4); 

// C:\Users\hello\Desktop\path
// C:\Users\hello\Desktop\path\img\so\about
// C:\Users\hello\Desktop\path\img\so\about
// C:\img\so\about
// C:\about

```

## 结论
- 使用join可以避免路径中使用 ./ 或者 /的问题，都能正确拿到路径。
- 使用resolve避免在衔接是出现/，因为那样它会跳进根目录。
