---
layout: post
title: Ruby 对数组的基本操作
date: 2014-11-10
author: jyootai
disqus: y
share: y
categories: blog
---

数组是 Ruby 中基本的数据类型，对其操作也很普遍，有时为了达到某个操作效果，需要查一查文档，于是索性将其最基本的操作方法总结下来，以后按需所取。

---

Ruby 数组中的元素可以是不同数据类型，这一点让处理各种数据也变得非常简单快捷。

和其它语言一样的地方一样的是，Ruby 数组中第一个值索引为0，最后一个值的索引为 size-1 或者是 length-1,和其它语言或许不一样的地发是，Ruby 也可以用负值索引取值，赋值索引将从数组的末尾开始计数，最后一个值的索引为-1，倒数第二个为-2，以此类推。下面来看看对数组操作的一些基本操作方法。

---

### 数组的符号操作

Ruby 可以使用 `+` 操作符来连接两个数组,使用 `+` 操作符将创建一个新数组，它包含了左右两个数组的所有元素。同时也可使用 `<<` 操作符在一个数组后面添加元素：

{% highlight ruby %}
[1,2,3,4] + [5,6]			#=> [1,2,3,4,5,6] 
a=[]			#=> 建一个新数组
a << 1		#=> a=[1]
a<< 2 << 3	#=> a=[1,2,3]

{% endhighlight %}

使用 `-` 操作符从一个数组中减掉另一个数组。它首先生成左侧数组的一份拷贝，然后从该拷贝中删除所有出现在右侧数组中的元素：

{% highlight ruby %}
[1,2,3,4,5,6] - [5,6]		#=> [1,2,3,4] 
a=[1,2,3,4]			#=> 给数组a赋值
b=[1,2]				#=> 给数组b赋值
a - b				#=> 数组a - b
a					#=> a=[1,2,3,4] 执行 - 后，数组a的值不变
{% endhighlight %}

布尔操作符 `|` 和 `&` ，它们分别用两个数组之间的并集和交集运算。 `|` 操作符会合并那两个作为其实参的数组，然后从结果中去除所有重复的元素。 `&` 操作符将返回一个仅包含了那些同时出现在两个数组中的元素的数组，返回的数组中也不包含任何重复的元素：

{% highlight ruby %}
a = [1,1,2,2,3,3,4,5,6]
b = [3,4,4,5,6,6,7,7,8]
a | b			#=> [1, 2, 3, 4, 5, 6, 7, 8]
b | a			#=> [3, 4, 5, 6, 7, 8, 1, 2]
a & b		#=> [3,4,5,6]
b & a		#=> [3,4,5,6]
{% endhighlight %}

###数组的其它方法操作

Ruby 除了上面所提到的强大操作，也提供了其它强大方便的操作方法:

`clear` 方法，删除数组中的所有元素 
{% highlight ruby %}
a = [ "a", "b", "c", "d", "e" ] 
a.clear		#=> []
a			#>[]
{% endhighlight %}

`collect` 方法，对数组中的每一个元素进行遍历，block中对元素的操作将改变元素的值,但其本身元素值不变。
{% highlight ruby %}
a = [ "a", "b", "c", "d", "e" ] 
a.collect {|x| x + "G" } # => ["aG", "bG", "cG", "dG"] 
a				#>  [ "a", "b", "c", "d", "e" ] 
{% endhighlight %}

`compact` 方法，压缩数组，即删除数组中所有值为nil的元素。 
{% highlight ruby %}
[ "a", nil, "b", nil, "c", nil ].compact 		# => ["a", "b", "c"] 
{% endhighlight %}

`concat` 方法，将第二个数组中的元素添加在第一个数组末尾，组成新数组。
{% highlight ruby %}
[ "a", "b", "c"].concat(["d","e"]) 		# => ["a", "b", "c","d","e"] 
{% endhighlight %}

`count` 方法，计算数组中等于某个值的元素有几个。
{% highlight ruby %}
[1, 2, 3, 4].count(2) 					# => 1 
[1, 2, 2, 3, 4].count(2) 				# => 2 
[1, 2, 3, 4].count {|element| element > 2 } # => 2
["a","b","b","c","d"].count("b") 			# => 2 
{% endhighlight %}

`join` 方法，将数组中的元素转换成字符串。如果有参数，则在每个元素后添加该参数。
{% highlight ruby %}
[ "a", "b", "c" ].join 		# => "abc" 
[ "a", "b", "c" ].join("-") 	# => "a-b-c" 
{% endhighlight %}

`replace` 方法，用新数组元素替换旧数组元素。 
{% highlight ruby %}
a = ["a", "b", "c"]
a.replace(["x", "y", "z"])	#=> ["x", "y", "z"]
a					#=> ["x", "y", "z"]
{% endhighlight %}

`reverse` 方法，颠倒数组元素。
{% highlight ruby %}
a = ["a", "b", "c"]
a.reverse 		#=> ["c", "b", "a"]
{% endhighlight %}

`shift` 方法，从数组起始位置删除n个元素，并将他们返回。若删除的是一个，则返回字符串。若删除两个以上元素，则返回这n个组成的新数组。原数组被改变。 
{% highlight ruby %}
a = ["a", "b", "c", "d", "e" ]
a.shift 		#=> "a"
a			#=> ["b", "c", "d", "e"] 
a.shift(2)		#=> ["b", "c"]
a			#=> ["d", "e"]
{% endhighlight %}

`unshift` 方法，在数组起始位置加入元素，原数组元素往后移，原数组改变。
{% highlight ruby %}
 a = ["b", "c", "d", "e"]
 a.unshift("a")		#=> ["a", "b", "c", "d", "e"]
 a				#=> ["a", "b", "c", "d", "e"]
 a.unshift(1,2)		#=> [1, 2, "a", "b", "c", "d", "e"]
 a				#=> [1, 2, "a", "b", "c", "d", "e"] 
{% endhighlight %}

`shuffle` 方法，将随机改变数组内元素顺序，原数组不变。
{% highlight ruby %}
a=["a", "b", "c", "d"]
a.shuffle		#=>  ["c", "d", "b", "a"]
a			#=> ["a", "b", "c", "d"] 
{% endhighlight %}

`transpose` 方法，将数组看成矩阵，行与列进行交换，原数组不变。
{% highlight ruby %}
a = [[1,2], [3,4], [5,6]]
a.transpose   	#=> [[1, 3, 5], [2, 4, 6]]
a			#=> [[1,2], [3,4], [5,6]] 
{% endhighlight %}

`flatten` 方法，返回一个新的一维数组。也就是说，对于每一个数组类的元素，提取他的元素到一个新的数组。可选的参数决定了将递归的程度，原数组不变。
{% highlight ruby %}
a = [ 1, 2, 3 ]           #=> [1, 2, 3]
b = [ 4, 5, 6, [7, 8] ]   #=> [4, 5, 6, [7, 8]]
c = [ a, b, 9, 10 ]       #=> [[1, 2, 3], [4, 5, 6, [7, 8]], 9, 10]
c.flatten                 #=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
a = [ 1, 2, [3, [4, 5] ] ]
a.flatten(1)              #=> [1, 2, 3, [4, 5]]
{% endhighlight %}

`sort` 方法，返回一个新的排好序的数组，用于排序的比较将使用 `<=>` 操作符或者一个可选的代码块,代码块必须实现 a 与 b 的比较， 当 a 小于 b 返回 -1，当相等时返回0，当 a 大于 b 时，返回1。
{% highlight ruby %}
a = [ "d", "a", "e", "c", "b" ]
a.sort                    #=> ["a", "b", "c", "d", "e"]
a.sort { |x,y| y <=> x }  #=> ["e", "d", "c", "b", "a"]
{% endhighlight %}

`values_at` 方法，返回多个索引位置的值。
{% highlight ruby %}
a = %w{ a b c d e f } 	#=> ["a", "b", "c", "d", "e", "f"]
a.values_at(1, 3, 5) # => ["b", "d", "f"] 
a.values_at(1, 3, 5, 7) # => ["b", "d", "f", nil] 
a.values_at(-1, -3, -5, -7) # => ["f", "d", "b", nil] 
a.values_at(1..3, 2...5) # => ["b", "c", "d", "c", "d", "e"] 
{% endhighlight %}

`uniq` 方法，去除数组中相同的元素，原数组不变。
{% highlight ruby %}
a = [ "a", "a", "b", "b", "c" ] 
a.uniq 		#=> ["a", "b", "c"] 
{% endhighlight %}

---

以上方法只是操作数组方法中的一部分，不过这些方法都是比较常用且难记的，因此总结此处以便查看。






















