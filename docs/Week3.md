# Week-3 Assignment

Status: Done
Tags: Express, HTTP, Node.js, npm

[Week-3 Note](https://www.notion.so/Week-3-Note-ba7e4aa3a3314bea9bfe0394749ed9dd)

[remote-assignments/Week-3/Assignment at main · fockspaces/remote-assignments](https://github.com/fockspaces/remote-assignments/tree/main/Week-3/Assignment)

### Assignment architecture :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled.png)

### Assignment 1: Your First Web Server

**思路** 

基本的Express建立，這裡port設3000可以防止和 HTTP(Port 80) and HTTPS(Port 443)衝突

reference :

**[Significance of port 3000 in Express apps - node.js](https://stackoverflow.com/questions/37929173/significance-of-port-3000-in-express-apps)**

### Assignment 2: Build Backend API for Front-End

**思路** 

這裡透過url傳入的參數都會存到req.params內，將parameter轉換為數字後，再判斷是否為整數。

如果是 : renderedText = 等差級數和

如果不是 : renderedText = error message

> 📄 ****[How to use the Fetch API with async/await](https://rapidapi.com/guides/fetch-api-async-await)****

**Tips**

1. **Params轉換成數字**

這裡可以用parseInt()或單純前綴補上+號的方法，我認為後者更好，分析如下:

```jsx
1. parseInt() : parseInt(’12d’) ⇒ 12 ⇒ number type

2. + : +’12d’ ⇒ NaN ⇒ not a number
```

前者無法分辨是否為純數字，而是將數字部分轉為Number type

後者可以分辨純數字，較符合此題需求

> **(Optional) Think about what will happen when N is very large.**
> 

Since the time complexity of the for-loop method is O(N), the runtime becomes larger when N becomes large.

We can solve this problem mathematically by simply applying the arithmetic series formula (n/2)⋅(a₁+aₙ) to reduce the time complexity to O(1), which only makes one operation performed per time.

> **Issue : 為何Fetch API無法順利執行redirecting**
> 

**Axios :**

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%201.png)

**Fetch :**

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%202.png)

**程式邏輯 :** 

在sending request後，server端會判斷數字是否合法，若合法則送回XML file，不合法則server會render “error page”。

**不能載入頁面的可能原因 :** 

1. axios內建error handler，當發現server送回的訊息無法解析成XML(or JSON)時，他會繼續執行server的指令(也就是rendering page)。
2. 而Fetch則是會因無法解析JSON而throw error，將error catch之後可以得到以下訊息 : 

> uncaught (in promise) SyntaxError: Unexpected token '<', "<!DOCTYPE "... is not valid JSON
> 

*render會將整個page的原始碼送回去，導致Fetch無法以json()解析*

如果想繼續render page，就必須將執行權交回server，但這裡不清楚該如何做到，因此我直接改call axios function。等之後學得更完整再回頭解決此問題。

### Assignment 3: Connect to Backend API by AJAX

**Tips :**

1. 將public folder下的所有static files cache住

```jsx
app.use(express.static('public'))
```

1. 與上面一樣，但新增一個virtual path ‘/static’

```jsx
app.use('/static', express.static('public'))
```

1. 要import module到browser，可以使用CDN

```jsx
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

**思路** 

1. 先用app.use(express.static("public")) render public folder中的index.html 
2. 以axios或XMLHttpRequest與Server Route連結，取得資料後修改至DOM element的innerHTML中
3. 製作Form表單，透過input.value取得想要的值，再用template literals嵌入URL中，最後回到步驟二修改element

**Todo**

- [x]  加入error catch middleware, routes folder

> 📄 [客製化error](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Error)

附註 : 因為/:myName佔在root route，這邊如果要客製化區分user / data會比較難
(例如我無法區分not found page是由data還是myName path而來，這會影響which page to render)
故我直接改為render page而非throw error來發送錯誤訊息
如果能將myName / data兩個routes路徑區分開，用express error handler集中處理會是比較好的做法

- [x]  改為render error/sucessful page

>📄 [**如何catch住404?**](https://stackoverflow.com/questions/6528876/how-to-redirect-404-errors-to-a-page-in-expressjs)

- [x]  新增未註冊重導頁面

### Assignment 4: HTTP Cookie

**思路**

1. 建立express server，並接受parpams參數 “myName”傳入
2. 建立signup page，判斷參數是否包含在cookies內，若無則direct to
3. signup 內建post method form，將input送至req.body後交給server
4. POST /trackName 接收到參數時，將name傳回browser cookie後，導回初始頁面

**Tips :** 

1. 必須加上此段，來正確接收傳入參數

```jsx
app.use(express.json());       // to support JSON-encoded bodies
app.use(express.urlencoded()); // to support URL-encoded bodies
```

1. res.redirect加上return，避免繼續執行下方程式碼

**驗收 :** 

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%203.png)

- [x]  確認當server關掉時，cookies是否都還在
- [x]  確認當chrome重啟時，cookies是否會消失

**To-do :**

1. 是否cookie可以接受<key, multi-value>型式? 如此一來只需查找該key中所有name即可
2. 更熟悉HTTP POST / GET method的使用，了解express router原理及應用(轉成MVC架構來設計)
3. 增加logout功能，並區隔登入登出畫面

ref **:**

[Day24 - Cookie在express上的應用-登入實作為例。 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10187343)

### Assignment 5: Algorithm Practice (Advanced Optional)

**思路**

之前已經練習過此題，在最初我的想法與brute force差不多，因為那時還沒有hashmap的概念，但後來在學double-pointer後我有試著用類似的概念去實作，寫在方法三

1. brute force
用兩層for迴圈比對所有cases，再判斷是否滿足條件後回傳即可。
時間複雜度 : O(N^2)
空間複雜度 : O(1)
2. **hashmap**
先建立hashmap以<value, index>來存nums的資料。
接著直接對每一個元素nums[i]查找map中是否有滿足num[i] + [ ] = target的值
意即 : map.get(target - num[i]) has value or not ?
因為答案只有一種，滿足條件即可直接return
時間複雜度 : O(N)
空間複雜度 : O(N)
3. **sort and limit**
將nums排序後，形成由小到大的排列數組
接著兩個指針left, right指向nums頭尾 : 

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%204.png)

如果sum < target ⇒ increase，否則decrease，直到target === sum為止
這樣時間複雜度為sort的時間，也就是O(N*log(N))
空間複雜度(假設in-place sorting)，為O(1)

> Note : 
特別注意，因為這裡使用in-place sort，所以無法取得原本的index，若要return真實index，則可建立map再映射回去，但這樣space-complexity會變為O(N)，不如方法二
> 

> 分析 : 處理多大的數據時會開始感受到效能差異?
> 

這裡用for loop迴圈來進行測試，調整function call的次數N來累計運行時間

**Bug1 : 重複測資**

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%205.png)

我拿下列test case去重複驗證，發現結果竟然是第一種方法最好

```
const nums = [2, 7, 15, 11];
const target = 9;
```

但在思考過後，發現因為在這情況，function_1可以馬上找到target並回傳

而其他兩者則是需另外做其他操作(set map, sort…)。

**To-do:**

- [x]  產生隨機測試集，自行比較三個程式的時間差異

[Google Colaboratory](https://colab.research.google.com/drive/1392Imlm8tnzNM4jhQtZBFWM1NiNxy63e?usp=sharing)

用python寫了random array來產生test cases，這裡用sample的方式來避免重複數字產生(增加target命中的機率)

N為array length，而非test cases numbers

在N = 100的情況 :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%206.png)

在N = 1000的情況 :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%207.png)

在N = 10000的情況 :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%208.png)

- [x]  作業將data改為json files

在N = 500的情況 :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%209.png)

在N = 5000的情況 :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%2010.png)

在N = 50000的情況 :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%2011.png)

**結論 :**

這次實驗沒有很成功，

難點在於想出各種edge case，進而得到best, worst, average的運行效能
隨機產生出的test cases會因為不具代表性，只能反映出特定情況下的效率，再多的cases總數也只是重複運算類似結果而已。

**ref:** 

[How to measure time taken by a function to execute](https://stackoverflow.com/questions/313893/how-to-measure-time-taken-by-a-function-to-execute)

### 

### TreeHouse :

![Untitled](Week-3%20Assignment%20462f7f9eeeb8448783130d189cb70ad2/Untitled%2012.png)