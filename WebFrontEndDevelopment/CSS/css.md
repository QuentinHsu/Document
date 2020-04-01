# CSS

## 水平居中

### 行内元素

```
text-align: center;
```

### 块级元素

- 确定宽度的块级元素

    1.  margin 和 width 实现
        ```
            margin: 0 auto;
        ```
    2.  绝对定位和 `margin-left: -width/2`，

        前提是父元素 `position：relative`
