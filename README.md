# ShopifyTemplateLanguageTech
Shopify 模板开发教程
shopify 开发教程
==============
官方教程：[https://www.shopify.com/partners/blog/topics/learning-liquid](https://www.shopify.com/partners/blog/topics/learning-liquid)
-------
>本文引用于[https://webdesign.tutsplus.com/tutorials/getting-started-with-liquid-shopifys-template-language--cms-19747](https://webdesign.tutsplus.com/tutorials/getting-started-with-liquid-shopifys-template-language--cms-19747)
#什么是液体？
如果您不熟悉模板语言的概念，我经常将其描述为商店中的数据与发送到浏览器的HTML模板之间的桥梁。

通过使用一些简单易读（易于记忆）的构造，我们可以访问我们商店中的数据（例如产品标题，集合描述，一组产品图像或博客文章），并将这些数据直接输出到我们的模板中。其中一个主要好处是我们不需要知道该数据是什么 - 而只需要知道我们在每个模板中都可以访问哪些变量。
#液体如何工作？
正如本系列第一部分所讨论的，Shopify根据当前请求的URL决定发送给浏览器的模板。例如，如果URL是
[http://shopify-for-designers.myshopify.com/collections/cups，Shopify](http://shopify-for-designers.myshopify.com/collections/cups?ref=envato)将呈现该collections.liquid模板。
                                                                                                                                             

一旦Shopify制定出相关模板进行渲染，它将解析模板（及其外部布局文件）寻找Liquid占位符。遇到这些问题时，Shopify会将Liquid代码与商店中的相关数据进行替换。

关于模板语言的另一种思考方式就像在文本编辑器中的“查找和替换”。在这种情况下，Shopify平台会搜索所有Liquid占位符，然后用商店中的数据替换它们。然后将最终构建的文档作为HTML发送到浏览器。

如果这是你第一次进行模板化，它可能会首先感受到一个小外星人，但你很快就会掌握它。

#占位符
甲占位符是一个代码段时，这将最终被替换模板被发送给浏览器。

Liquid中有两种占位符。第一个是用双括号{{ }}表示输出，第二个{% %}用括号表示逻辑。

以下是您通常可以在微型模板中找到的输出占位符的简单示例product.liquid：
######&lt;h2>{{ product.title }}&lt;/h2>
呈现时，将输出当前查看的产品的名称以代替该名称{{ }}，例如：
######&lt;h2>Keir's Coffee Cup&lt;/h2>
输出，除非用过滤器操作（我们稍后会看到）仅仅是用商店中的文本替换占位符的情况。
#逻辑和循环
除了使我们能够从我们的商店中获取数据，并在我们的模板显示它，如上文所示，液体也能精确控制什么是显示在使用逻辑结构和循环我们的模板。

例如，我们可以选择显示不同的HTML片段，具体取决于当前查看的产品是否有货。

我们也可以使用Liquid多次输出相同的代码 - 例如一系列产品图像。使用循环可以让我们用几行Liquid代码输出与产品相关的所有产品。

液体是非常强大的，虽然你可能认为我们正在进入编程领域，但我相信你会很快拿起它。
#液体基础
现在您已经对Liquid的工作原理有了一个基本的了解，让我们来看看四个关键特性以及它们如何与主题开发相关联。
###产量
如前所述{{ }}，.liquid文件中的双括号表示输出占位符。以下是您经常遇到的两个示例：
- {{ shop.name }}
- {{ product.description }}

输出允许我们从我们的商店中提取特定的数据到我们的模板中，顾名思义，输出它代替Liquid占位符。

假设我的商店被称为“凯尔咖啡商场”。如果我要使用{{ shop.name }}液体标签，Shopify将获取我店铺的名称，并将我的商店名称的液体占位符直接替换为我的模板作为HTML。

同样，如果我们{{ product.description }}在我们的product.liquid模板中使用输入所见即所得编辑器中的特定产品的任何文本，都将输出{{ product.description }}占位符的位置。

注意：所见即所得的编辑器会输出格式化的HTML，所以你不需要{{ product.description }}用任何HTML元素来包装，比如a <p>。

可以用这种方式输出任何变量，无论它是全局变量（可用于主题中的每个单独模板）还是模板级变量（仅可用于特定模板）都可以输出。其他例子包括：


* {{ shop.description }}
* {{ product.title }}
* {{ collection.title }}
* {{ collection.description }}
有关您可以在主题中输出的变量的完整列表，我强烈建议您为Mark Dunkley的备忘单添加书签。我发现自己每天都在使用它。

总而言之，液体输出非常类似于“查找和替换”。在渲染模板时，Shopify将会去查找Liquid输出标签的所有实例，并将其替换为商店中的相关数据。

您还会从这些示例中注意到Liquid使用点语法来访问数据。点之前的项目是变量，而后面的项目是该变量的属性。例如，我们上面的商店变量同时具有名称和描述属性。

#逻辑
让我们进入Liquid逻辑。虽然对于首次使用的用户而言，稍微复杂一些，但是一旦您尝试了自己的逻辑标签，就不难理解了。

液体输出占位符允许我们获取数据并将其显示在我们的模板中液体逻辑标签允许我们控制模板的流动。与输出标签逻辑标签在你的模板包含不会造成任何直接呈现的，而它们使我们能够控制什么的呈现方式。

我用来说明如何使用液体逻辑的典型示例是突出显示产品何时售罄。以下示例通常可以在product.liquid微型模板中找到：
* {% if product.available %}
* This product is available
* {% else %}
* Sorry, this product is sold out
* {% endif %}
正如你将会看到液体逻辑的语法与输出略有不同。而不是{{ }}我们使用的分隔符{% %}。

在上面的例子中，我们控制的是使用简单的输出到我们的模板if，else，endif语句。在很多方面，if陈述就像问题。

在上面的例子中，如果我们的if陈述问题的答案是true我们呈现“This product is available”这个词，那么如果它是false我们的模板继续并输出我们的{% else %}子句之后的文本- 在这种情况下"Sorry, this product it sold out"。

你会发现自己if在Shopify主题开发中使用了很多语句。这是帮助你理解的另一个例子：
* {% if cart.item_count > 0 %}
* <p>You have {{ cart.item_count }} item(s) in your cart</p>
* {% else %}
* <p>There's nothing in your cart :( Why not have a <a href="/products">look at our product range</a></p>
* {% endif %}
此示例演示了一种方法，可以显示访客购物车中的物品数量，也可以输出指向产品的链接。
#运营商的快速说法
你会注意到在这个例子中我们使用的是大于>运算符。由于cart.item_count变量返回当前用户购物车中的物品数量，我们可以检查它是否大于零，即它中包含物品。

如果返回，true我们可以输出带有当前项目数的消息，否则我们可以输出<p>There's nothing in your cart :( Why not have a <a href="/products">look at our product range</a></p>。

您可以访问Liquid的各种操作员，其中很多您会经常使用：
* == 等于
* != 不等于
* &gt; 比...更棒
* < 少于
* &gt;= 大一点或相等
* <= 少一点或相等
* or 这个或那个
* and 必须是这个和那个
* contains 包括在字符串上使用的子字符串，或在数组上使用的元素

#循环
接下来让我们把注意力转向Liquid循环的概念。

如果您已经完成了任何形式的基本编程，循环数据的概念将非常熟悉。使用循环，通常称为a for loop，允许我们在模板中输出已知次数的相同代码。

让我们来看看Shopify主题中的一个例子，以帮助巩固这个概念：

* {% for image in product.images %} 
+ &lt;img src="{{ image | product_img_url: 'small' }}">
- {% endfor %}

在此示例中，通常在product.liquid微模板中找到该示例，我们使用循环输出与当前查看的产品关联的每个图像。让我们分解成几个步骤来充分理解它。

####第1步：{％for product.images％中的图片}
我们的开放线向我们介绍了Liquid的收藏理念。与我们在Liquid 中第一部分收集的产品收集不同。在这方面这是一个不幸的命名惯例，所以我喜欢将液体收集称为液体收集，以避免混淆。

Shopify主题中的Liquid集合可以采用多种形式，但product.images上面使用了一个很好的示例。液体收集很容易发现，因为它通常采用复数形式 - images如上所述。在我们的例子中，我们正在处理与产品相关的所有图像的Liquid集合。

另一个例子是product.variants。这将返回一个包含所有产品变体的详细信息的对象，以备我们的模板循环使用。如果您需要产品变体的初级产品，我们会在第一部分中进行讨论。

您还会注意到我们正在使用该词image来表示循环中的当前项目。每次我们循环时，我们image都会依次访问与每个图像相关的数据。当然这在每个循环中都会有所不同。

还值得注意的是，我们不需要知道会发生多少次循环。在没有更多图像循环后，Shopify将继续并呈现模板的下一部分。
####第2步：<img src =“{{image | product_img_url：'medium'}}”/>
我们的代码的第二行是HTML的一部分，也是Liquid的一部分。您会注意到该src属性被填充了一个Liquid输出标签。我们将看看由|字符表示的过滤器，但接下来这个简短的构造将使用我们的循环中当前图像的“小”版本的完全限定URL来填充src属性。
####第3步：{％endfor％}
我们例子的最后一行是我们的结束语endfor。这有效地关闭了将在循环内呈现的任何代码。

如果我们在product.images对象中有三个图像，最终输出将如下所示：
* &lt;img src="//cdn.shopify.com/s/files/1/0222/9076/products/il_fullxfull.296506684_small.jpg?v=1368007899" alt="" />
* &lt;img src="//cdn.shopify.com/s/files/1/0222/9076/products/moustache-mugs_by_peter-bruegger_1_small.jpg?v=1370429684" alt="" />
* &lt;img src="//cdn.shopify.com/s/files/1/0222/9076/products/tumblr_lhr5huUxXL1qfhlb1o1_500_small.jpg?v=1370429684" alt="" />
循环是非常有用的，你会在主题开发中每天遇到的东西。输出图像和产品变体是两个常见的例子。
#过滤器
我之前提到了与我们的循环示例有关的过滤器，所以让我们进一步详细了解一下它们的工作原理。

过滤器与输出标签一起使用。他们的目的是以某种方式操纵数据，以便更改格式。一个很好的例子是日期过滤器：

* {{ article.published_at | date: '%d %B %Y' }}
如果没有过滤器，Shopify只会以它存储在数据库中的格式输出博客文章的发布日期 - 这可能不是人类可读的。然而，通过添加|日期过滤器和我们可以自己操作的格式。

我们在左边开始一段数据，在这个例子中是一个日期，并且通过使用过滤器，它的另一侧发生了变化。实质上，这是过滤器的唯一目的。它需要一段数据，并以某种方式操纵它，以使其形式发生变化。

这是另一个例子：

* {{ 'style.css' | asset_url | stylesheet_tag }}
这里我们使用了两个过滤器，最终目的是在我们的布局文件中创建一个完全形成的样式元素。

我们从左侧开始使用CSS文件的名称，并首先应用asset_url过滤器。这是一个非常有用的过滤器。由于我们不知道我们的style.css文件位于Shopify网络的哪个位置（除了我们的主题中的资产文件夹），我们需要Shopify填充文件路径。

这是asset_url过滤器的目的。style.css在本例中，它将采用我们的文件的名称，并在商店资产文件夹的前面添加完整路径。值得注意的是，它不检查文件是否存在。

以下是输出时的外观：

- //cdn.shopify.com/s/files/1/0222/9076/assets/style.css
链中的最后一个过滤器stylesheet_tag采用这个URL并将其封装在一个样式元素中，然后输出到我们的布局文件中。最终的结果如下：
* &lt;link href="//cdn.shopify.com/s/files/1/0222/9076/t/10/assets/style.css?756" rel="stylesheet" type="text/css"  media="all"  />
每个过滤器都会接受其前一个过滤器的输出，并对其进行修改。当没有更多的过滤器将数据传入时，结果会以HTML形式输出到模板中。

有很多真正有用的过滤器，这里只是你会发现自己使用的几个：
* [ASSET_URL](http://docs.shopify.com/themes/filters/asset-url?ref=envato)
* [stylesheet_tag](http://docs.shopify.com/themes/liquid-basics/output#stylesheet-tag?ref=envato)
* [script_tag](http://docs.shopify.com/themes/liquid-basics/output#script-tag?ref=envato)
+ [日期](http://docs.shopify.com/themes/liquid-basics/output#date?ref=envato)
+ [变复数](http://docs.shopify.com/themes/liquid-basics/output#pluralize?ref=envato)
+ [更换](http://docs.shopify.com/themes/liquid-basics/output#replace?ref=envato)
- [处理](http://docs.shopify.com/themes/liquid-basics/output#handle?ref=envato)
- [钱和money_with_currency](http://docs.shopify.com/themes/liquid-basics/output#money-with-currency?ref=envato)
- [product_img_url](http://docs.shopify.com/themes/filters/product-img-url?ref=envato)
- [链接到](http://docs.shopify.com/themes/liquid-basics/output#link-to?ref=envato)

#下一步

在本教程中，我们经历了相当多的研究。我们查看了Liquid及其与HTML微型模板和布局文件的关系，并着眼于四个关键概念 - 输出，逻辑，循环和过滤器。
