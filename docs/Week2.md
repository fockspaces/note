# Week-2 Assignment

Status: Done
Tags: JQuery, JavaScript

[Week-2 Note](https://www.notion.so/Week-2-Note-f7fdc16d0b214b159763d71e722a2cc8)

[remote-assignments/Week-2 at main · fockspaces/remote-assignments](https://github.com/fockspaces/remote-assignments/tree/main/Week-2)

### Assignment 1: Function and Array

max : 先令ans = nums[0]，用for loop不斷更新最大值

findPosition : for loop過程，找到target即return ans，如此能回傳第一個出現的index

 

### Assignment 2: Function, Array, and Object

先對product price做summation，之後return sum / data.size即可

### Assignment 3: Data Manipulation

主要用hashmap來實作，以英文字母做為key

第一題用累加形式記錄count

第二題以value值進行summation

### Assignment 4: HTML DOM and Event Handling

website : 

[Fockspace](https://fockspaces.github.io/remote-assignments/Week-2/Assignment-4/)

### Request 1: Click to Change Text.

Select Welcome的box，並用eventListener來觸發事件

當被點擊時，修改innerHTML為"Have a Good Time!".

### Request 2: Click to Show More Content Boxes.

與前者做法類似，這裡可以有兩種方法去實作display的效果

1. 新增hidden class，將物件.classList.remove("hidden")

```
.hidden {
  visibility: hidden;
  opacity: 0;
}
```

1. 使用style.display = ‘none’
這麼做的好處是，隱藏時不會占用畫面大小

```jsx
content.style.display = 'none'
```

### Assignment 5: Algorithm Practice (Advanced Optional)

這裡用到binary search，我習慣使用開區間查找，如此若未能找到，最後指標的值會是lower_bound(即待插入位置)

這邊設置while迴圈，左指標指向頭，右指標指向尾
每次都用中間點與target做比較，每次查找過程會將待查找數組降為N/2
因此最多只需log(N)次即可完成搜尋

### Assignment 6: HTML DOM and Event Handling with jQuery (Advanced Optional)

Website:

[](https://fockspaces.github.io/remote-assignments/Week-2/Assignment-6/)

重新將Assignment 4 refactor成JQuery的形式

### 課程進度

![Untitled](Week-2%20Assignment%203b26ea1ca57d4733a7191e2e6e5cac30/Untitled.png)

2023/01/12

![Untitled](Week-2%20Assignment%203b26ea1ca57d4733a7191e2e6e5cac30/Untitled%201.png)