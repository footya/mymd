#JSTL常用语法学习#
*footya@qq.com* 2014/3/26

##fn##
*fn:contains(string, substring)*
>假如参数string中包含参数substring，返回true
<pre>&lt;c:if test="${fn:contains(name, searchString)}"&gt;</pre>

*fn:containsIgnoreCase(string, substring)*
>假如参数string中包含参数substring（忽略大小写），返回true
<pre>&lt;c:if test="${fn:containsIgnoreCase(name, searchString)}"&gt;</pre>

*fn:endsWith(string, suffix)*
>假如参数 string 以参数suffix结尾，返回true
<pre>&lt;c:if test="${fn:endsWith(filename, ".txt")}"&gt;</pre>

*fn:escapeXml(string)*
>将有非凡意义的XML (和HTML)转换为对应的XML character entity code，并返回
例如： <字符应该转为&lt; 
<pre>${fn:escapeXml(param:info)}</pre>

*fn:indexOf(string, substring)*
>返回参数substring在参数string中第一次出现的位置
<pre>${fn:indexOf(name, "-")}</pre>

*fn:join(array, separator)*
>将一个给定的数组array用给定的间隔符separator串在一起，组成一个新的字符串并返回。
<pre>${fn:join(array, ";")}</pre>

*fn:length(item)*
>返回参数item中包含元素的数量。参数Item类型是数组、collection或者String。假如是String类型,返回值是String中的字符数。
<pre>${fn:length(shoppingCart.products)}</pre>

*fn:replace(string, before, after)*
>返回一个String对象。用参数after字符串替换参数string中所有出现参数before字符串的地方，并返回替换后的结果
<pre>${fn:replace(text, "-", "&#149;")}</pre>

*fn:split(string, separator)*
>返回一个数组，以参数separator 为分割符分割参数string，分割后的每一部分就是数组的一个元素
<pre>${fn:split(customerNames, ";")}</pre>

*fn:startsWith(string, prefix)*
>假如参数string以参数prefix开头，返回true
<pre>&lt;c:if test="${fn:startsWith(product.id, "100-")}"&gt;</pre>

*fn:substring(string, begin, end)*
>返回参数string部分字符串,从参数begin开始到参数end位置，包括end位置的字符
<pre>${fn:substring(zip, 6, -1)}</pre>

*fn:substringAfter(string, substring)*
>返回参数substring在参数string中后面的那一部分字符串
<pre>${fn:substringAfter(zip, "-")}</pre>

*fn:substringBefore(string, substring)*
>返回参数substring在参数string中前面的那一部分字符串
<pre>${fn:substringBefore(zip, "-")}</pre>

*fn:toLowerCase(string)*
>将参数string所有的字符变为小写，并将其返回
<pre>${fn.toLowerCase(product.name)}</pre>

*fn:toUpperCase(string)*
>将参数string所有的字符变为大写，并将其返回
<pre>${fn.UpperCase(product.name)}</pre>

*fn:trim(string)*
>去除参数string 首尾的空格，并将其返回
<pre>${fn.trim(name)}</pre>

--------------------------------------------------------------------------
##&lt;c:foreach&gt;用法##
###语法###
**语法1：迭代一集合对象之所有成员**
<pre>
&lt;c:forEach [var="varName"] items="collection" [varStatus="varStatusName"] [begin="begin"] [end="end"] [step="step"]&gt;
&lt;/c:forEach&gt;
</pre>
**语法2：迭代指定的次数**
<pre>&lt;c:forEach [var="varName"] [varStatus="varStatusName"] begin="begin" end="end" [step="step"]&gt;
    &lt;/c:forEach&gt;</pre>
###属性###
- var：迭代参数的名称。在迭代体中可以使用的变量的名称，用来表示每一个迭代变量。类型为String。
- items：要进行迭代的集合。
- varStatus：迭代变量的名称，用来表示迭代的状态，可以访问到迭代自身的信息。
- begin：如果指定了items，那么迭代就从items[begin]开始进行迭代；如果没有指定items，那么就从begin开始迭代。它的类型为整数。
- end：如果指定了items，那么就在items[end]结束迭代；如果没有指定items，那么就在end结束迭代。它的类 型也为整数。
- step：迭代的步长。
- current：当前这次迭代的（集合中的）项。
- index：当前这次迭代从0开始的迭代索引。
- count：当前这次迭代从1开始的迭代计数。
- first：用来表明当前这轮迭代是否为第一次迭代，该属性为boolean类型。
- last：用来表明当前这轮迭代是否为最后一次迭代，该属性为boolean类型。
- begin：begin属性的值。
- end：end属性的值
- step：step属性的值
###示例###
1. 循环遍历，输出所有的元素。
<pre>
&lt;c:foreach items="${list}" var="li"&gt;
    ${li}
&lt;/c:foreach&gt;
</pre>
>注意：items 用于接收集合对象，var 定义对象接收从集合里遍历出的每一个元素。同时其会自动转型。

2. 循环遍历，输出一个范围类的元素。
<pre>
&lt;c:foreach items ="${lis}" var = "li " begin="2" end ="12"&gt;
    ${li}
&lt;/c:foreach&gt;
</pre>
>注意：begin 定义遍历的开始位置，end定义遍历的结束位置。begin 和end的引号必须写。

3. 循环遍历，输出除某个元素以外的元素或输出指定元素。
<pre>
&lt;c:foreach items="${list}" var ="li" varStatus="status"&gt;
    &lt;c:if text="${status.count==1}>
${"第一个元素不要"}
    &lt;/c:if&gt;
${li}
&lt;/c:foreach&gt;
</pre>
>注意：varStatus 表示迭代变量的名称，用来表示迭代的状态，可以访问到迭代自身的信息，count为循环一个计算器。

4. 循环遍历，输出第一个或最后一个元素。
<pre>&lt;c:foreach items="${list}" var ="li" varStatus="status"&gt;
    &lt;c:if text="${status.first}"&gt;我是第一个元素&lt;/c:if&gt;
    &lt;c:if text="${status.last}"&gt;我是最后一个元素&lt;/c:if&gt;
    &lt;/c:foreach&gt;</pre>
>注意：first表示如果是一个元素，则返回ture,反之则返回false
           last 表示如果是最后一个元素，则返回ture,反之则返回false。

5. 循环遍历，按指定步长输出。
<pre>&lt;c:foreach items="list" var ="li" step="2"&gt;
    ${li}
    &lt;/c:foreach&gt;</pre>
>注意：step为循环的步长。每次隔两个单位输出一个。如：1、3、5、==

-------------------------------------------------------------------------------------
##&lt;c:choose&gt;##
>&lt;c:choose&gt;本身只当做 &lt;c:when&gt; 和 &lt;c:otherwise&gt;的父标签。

<pre>
&lt;c:choose&gt;
            &lt;c:when test=&quot;${typename.name == null }&quot;&gt; 
                &lt;h3&gt;请在左边选择你遇到的问题：&lt;/h3&gt;
                        &lt;p&gt; 
                        1.请详细描述您遇到的问题&lt;br /&gt;
                         &lt;b&gt;&lt;/b&gt;
                        2.如果可以，请尽可能的给我
                        们提供完善的资料，这样有助于我们更快的帮您解决问题。&lt;br /&gt;
                         &lt;b&gt;&lt;/b&gt;                        &lt;/p&gt;
            &lt;/c:when&gt;
            &lt;c:otherwise&gt;
                &lt;h3&gt;${ typename.name }：&lt;/h3&gt;
            &lt;/c:otherwise&gt;
        &lt;/c:choose&gt;
</pre>
--------------------------------------------------------------------------------------
##&lt;c:out&gt;##
>标签的作用是用来显示表达式的值。它的作用是用来替代通过JSP内置对象out或者<%=%>标签来输出对象的值

###语法###
<pre>
 &lt;c:out value=&quot;expression&quot; default=&quot;expression&quot; escapeXml=&quot;boolean&quot;/&gt;
</pre>
###属性###
- value：用来定义需要求解的表达式。
- default：缺省值。当求解后的表达式为null或者String为空时将打印这个缺省值。
- escapeXML：这个属性是可选的。用于指定在使用<c:out>标记输出诸如“<”、“>;”和“&”之类的字符（在 HTML 和 XML 中具有特殊意义）时是否应该进行转义。如果将 escapeXml 设置为true，则会自动的进行编码处理。

