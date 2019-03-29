# JavaScript

## 个人收集整理常用的JS技巧

### JavaScript把字符串(yyyyMMdd)转换成日期格式（yyyy-MM-dd）

```js
{{ ordersItem.ordersId.replace(/(\d{4})(\d{2})(\d{2})(\d{2})(\d{2})(\d{5})/, '$1-$2-$3 $4:$5') }}
```
