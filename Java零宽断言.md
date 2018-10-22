1. 断言
> 类似^代表开头，$代表结尾，\b代表单词边界一样，匹配某些位置的就叫断言。所谓位置：指字符串（每行）第一个字符左边、最后义字符右边以及相邻字符中间（假设文字从左到右）。
2. 零宽：
> 匹配过程不占用字符，所以称为零宽.
3. 正向，负向
> 能够匹配pattern称为正向，用=表示；不能够匹配pattern称为负向用！表示
4. 先行，后行
先行后行如果按照从左往右（从前到后）的次序比较好理解。先行断言，是当扫描指针位于某处时，引擎会尝试匹配指针还未扫过的字符，先于指针到达该字符，故称为先行。后行断言，引擎会尝试匹配指针已扫过的字符，后于指针到达该字符，故称为后行。
> * 先行：位置之后的字符串是否与pattern匹配
> * 后行：位置之前的字符串是否与pattern匹配

5. 正则表达式的先行断言和后行断言一共有4种形式
> 
> * (?=pattern) 零宽正向先行断言(zero-width positive lookahead assertion)
> * (?!pattern) 零宽负向先行断言(zero-width negative lookahead assertion)
> * (?<=pattern) 零宽正向后行断言(zero-width positive lookbehind assertion)
> * (?<!pattern) 零宽负向后行断言(zero-width negative lookbehind assertion)

6. 限制
> 括号里的pattern本身是一个正则表达式。但对2种后行断言有所限制，在Perl和Python中，这个表达式必须是定长(fixed length)的，即不能使用*、+、?等元字符，如(?<=abc)没有问题，但(?<=a*bc)是不被支持的，特别是当表达式中含有|连接的分支时，各个分支的长度必须相同。之所以不支持变长表达式，是因为当引擎检查后行断言时，无法确定要回溯多少步。Java支持?、{m}、{n,m}等符号，但同样不支持*、+字符。

7. 例子
`        System.out.println("varchar(25) NOT NULL".matches("(?<=varchar\\([\\d]?[\\d]?[\\d]?\\) )NOT NULL"));
`
```
        System.out.println("varchar(25) NOT NULL".matches("(?<=varchar\\([\\d]?[\\d]?[\\d]?\\) )NOT NULL"));
```
matches是不会匹配的，replace可以。前面对长度的限制可以通过例子的方式进行破解。
