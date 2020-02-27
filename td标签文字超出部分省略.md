# td标签文字超出部分省略

``` css
table { table-layout: fixed;} //必须，表格宽度不随文字增多而变长。

 td { white-space: nowrap;overflow: hidden;text-overflow: ellipsis;}
```

