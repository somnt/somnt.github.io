---
layout: post
title:  "TKinter Scroll Bar"
date:   2016-06-12 17:00:13 +0800
categories: python
tags:
- python  
- tkinter
---

### Scroll Bar with Text

{% highlight python %}
#/usr/bin/python2.7
from Tkinter import *
from Tkinter import ttk
root = Tk()

text = Text(root, width = 40, height = 10, wrap = 'word')
# wrap = 'word' 换行不拆分单词
text.grid(row = 0, column = 0)
scrollbar = ttk.Scrollbar(root, orient = VERTICAL, command = text.yview)
# yview 方法当滑动scroll时显示对应内容
scrollbar.grid(row = 0, column = 1, sticky = 'ns')
# ns -> north and south,为适应父widget的顶部的底部拉伸
text.config(yscrollcomannd = scrollbar.set)
# 使scrollbar可上下滑动显示对应内容位置

root.mainloop()
{% endhighlight %}

### Scroll Bar with Canvas --Drawing lines

{% highlight python %}
from Tkinter import *
from Tkinter import ttk

root = Tk()
canvas = Canvas(root, scrollregion = (0, 0, 640, 480), bg = 'white')
xscroll = ttk.Scrollbar(root, orient = HORIZAONTAL, command = canvas.xview)
yscroll = ttk.Scrollbar(root, orient = VERTICAL, command = canvas.yview)
canvas.config(xscrollcommand = xscroll.set, yscrollcomannd = yscroll.set)

canvas.grid(row = 1, column = 0)
xscroll.grid(row = 2, column = 0, sticky = 'ew')
yscroll.grid(row = 1, column = 1, sticky = 'ns')

def canvas_click(event):
  x = canvas.canvasx(event.x)
	y = canvas.canvasy(event.y)
  #canvas.canvasx与canvas.canvasy为确保canvas能注意到scrollbar的滑动，使得点能点在正确的位置上

	canvas.create_oval((x-5, y-5, x+5, y+5), fill = 'green')

canvas.bind('<1>', canvas_click)

root.mainloop()
{% endhighlight %}
