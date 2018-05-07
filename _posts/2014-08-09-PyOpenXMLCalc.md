---
layout: post
title: "PyOpenXMLCalc"
subtitle: "A python library to create OpenXML spreadsheets"
quote: false
image: false
video: false
comments: false
---

A python library to create OpenXML spreadsheets, so that Microsoft Excel, or every other program that supports this format (e.g. LibreOffice, Openoffice) can open a file created with this library.

Implemented features:

- create a blank workbook
- or open an existing xlsx file
- create a new sheet
- write into a cell
- write data in CSV format to sheet
- read from a cell
- read from a sheet line by line
- format tables with templates
- freeze a row
- conditional formatting (beginsWith, expression)
- save as *.xlsx

Requirements:

- Python 2\.4 - 2\.6

## Example

create a new sheet

{% highlight py %}
from PyOpenXMLCalc import *

workbook = Calc('Company','userName')
workbook.newSheet('Test')
workbook.selectSheet('Test')
{% endhighlight %}

import a list 

{% highlight py %}
l = list()
l.append(['A','B','C','D','E'])
for i in range(10):
    l.append(['A','OK' if i%2 else 'NOK','C','D','E'])
workbook.import_list('A1',l)
{% endhighlight %}

create a formated table

{% highlight py %}
ref = workbook.formatTable('A1','Table1',tableStyle='TableStyleMedium16')
{% endhighlight %}

define some colors 

{% highlight py %}
rgb_read = "FFFF0000"
rgb_green = "FF00B050"
rgb_orange = {'theme':'9'}
rgb_grey = {'theme':"1",'tint':"0.499984740745262"}
dxfId = workbook.getStyle(rgb_green)
{% endhighlight %}

conditional formating

{% highlight py %}
workbook.add_conForm_beginWith(Sqref('A2:A%s'%ref.end.rowID),dxfId,4,'A')
format_ = 'B2="OK"'
workbook.add_conForm_expression(Sqref('B2:B%s'%ref.end.rowID),dxfId,format_,4)
workbook.add_frozen_row(1)
{% endhighlight %}

save to file

{% highlight py %}
workbook.selectCell('B2')
workbook.save('Sample.xlsx')
{% endhighlight %}

{% include image.html url="/media/PyOpenXMLCalc/excel-sample1.png" description="excel screenshot" %}

For further examples please have a look at sample.py and sample-2.py
