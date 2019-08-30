#Elasticsearch

Elasticsearch中的数据大致可以分为两种类型:精确值和全文。

精确值就是它们听起来的样子。例如日期或用户ID，但也可以包含确切的字符串，如用户名或电子邮件地址。确切的值“Foo”不等于确切的值“foo”。2014年的确切值与2014-09-15不一样。
另一方面，全文指的是文本数据——通常是用某种人类语言编写的——比如一条推文的文本或一封电子邮件的正文。Elasticsearch中的数据大致可以分为两种类型:精确值和全文。

全文通常被称为“非结构化数据”，这是一个错误的名称——自然语言是高度结构化的。问题是自然语言的规则是复杂的，这使得计算机很难正确地解析它们。


- May is fun but June bores me.
- 五月很有趣，但六月让我厌烦。

它是指月份还是指人?

精确的值很容易查询。决策是二进制的——一个值要么匹配查询，要么不匹配。
这种查询很容易用SQL表达

```
WHERE name    = "John Smith"
  AND user_id = 2
  AND date    > "2014-09-15"
```

查询全文数据要微妙得多。我们不只是问这个文档是否匹配查询，而是问这个文档是否匹配查询?换句话说，该文档与给定查询的相关性如何?
我们很少想要完全匹配整个文本字段。相反，我们希望在文本字段中进行搜索。不仅如此，我们希望搜索能够理解我们的意图:

```
a search for "UK" should also return documents mentioning the "United Kingdom"
a search for "jump" should also match "jumped", "jumps", "jumping" and perhaps even "leap"
"johnny walker" should match "Johnnie Walker" and "johnnie depp" should match "Johnny Depp"
"fox news hunting" should return stories about hunting on Fox News, while "fox hunting news"should return news stories about fox hunting.
```

为了方便对全文字段进行此类查询，Elasticsearch首先分析文本，然后使用结果构建反向索引。我们将在接下来的两部分中讨论反向指标和分析过程。


---

>Elasticsearch 从入门到跑路   