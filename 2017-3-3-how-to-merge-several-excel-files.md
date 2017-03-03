## 如何合并多个excel?

> 写在前面：一直在探索比较好用的记笔记方式，先后用过备忘录、印象笔记、day-one等一些方式。我主要的需求是
>
> 1. 可以用markdown，代码高亮比较清晰易读
> 2. 可以记录记笔记的日期
> 3. 比较方便的管理方式
>
> 使用印象笔记的时间比较长，但是它不支持markdown，而且笔记数量一多，就会变得很难以管理。day-one虽然支持markdown，但是代码高亮的部分永远没有缩进，而且很难空行。虽然day-one用日历管理笔记的方法挺好的，但是没有文件夹的功能，无法方便管理同一主题的笔记。所以。。最后还是回到同性交友网站惹(⁎⁍̴̛ᴗ⁍̴̛⁎)

今天早上做了一件事：合并多个excel，一共大概3600行。

百度经验指导我们用excel里面的宏计算来做，不过我的电脑一打开宏计算，excel就闪退了。。闪退了。。

所以这个方法不行，这个时候我想到的就是去抱python大腿啦

```python
import pandas as pd
```

写下这一行，心中充满力量， pandas用来做数据处理非常强大啊。```pd.read_excel```，没问题，能正确读取数据，可是```pd.to_excel```死活都报UnicodeDecodeError，尝试了各种各样的```encoding```都不行。

我就放弃了从excel -> excel，准备从excel -> csv -> excel

这下就很方便啦：首先读取excel文件，转换为一个个的csv文件

```python
#-*- coding=utf-8 -*-
import pandas as pd 
import glob
import os
from os.path import basename

for f in glob.glob('*-*.xls'):
	df = pd.read_excel(f,header = 2)
	base = os.path.basename(f)
	name = os.path.splitext(base)
	df.index = [name[0]] * len(df) #这里主要是为了给每一行数据增加来源文件的信息
	df.to_csv(name[0] + '.csv')
```

然后转换好了，在当前目录下，用linux:

```linux
cat *.csv > output.csv
```

一般从csv->excel，我都是用OpenOffice打开另存，这样很快就实现了合并多个excel > <
