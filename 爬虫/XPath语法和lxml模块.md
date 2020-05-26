# XPath语法和lxml模块
#爬虫

```python
from lxml import etree

wb_data = “””
        <div>
            <ul>
                 <li class=“item-0”><a href=“link1.html”>first item</a></li>
                 <li class=“item-1”><a href=“link2.html”>second item</a></li>
                 <li class=“item-inactive”><a href=“link3.html”>third item</a></li>
                 <li class=“item-1”><a href=“link4.html”>fourth item</a></li>
                 <li class=“item-0”><a href=“link5.html”>fifth item</a>
             </ul>
         </div>
        “””
html = etree.HTML(wb_data)
print(html)
result = etree.tostring(html)
print(result.decode(“utf-8”))
```

## 元素
```python

html = etree.HTML(wb_data)
html_data = html.xpath('/html/body/div/ul/li/a')
print(html)
for i in html_data:
    print(i.text)
```

## 属性

```python
html = etree.HTML(wb_data)
html_data = html.xpath('/html/body/div/ul/li/a/text()')
print(html)
for i in html_data:
    print(i)

```


