---
id: 366
title: Exporting dimensions to Excel from NX
date: 2018-07-28T17:42:18+05:30
author: Achyuthuni Sri Harsha
layout: post
guid: https://www.harshaash.com/?p=366
permalink: /exporting-dimensions-to-excel-from-nx/
categories:
  - NX Journalling
tags:
  - dimensions
  - excel
  - journaling
  - NX
---
<p style="text-align: left;">
  This blog is the third part of a <a href="https://www.harshaash.com/extracting-data-from-mechanical-models/">3 part series on NX journalling</a>
</p>

<p style="text-align: left;">
  The aim of this blog post is to open an excel window from NX and exporting properties from workPart.Dimensions to excel.
</p>

Continuing from the previous post, we could write the following program

The following code can also be found at <https://github.com/HarshaAsh/NXBasics>

> <p style="text-align: left;">
>   Option Strict Off<br /> Imports System<br /> Imports NXOpen<br /> Imports NXOpenUI
> </p>
> 
> <p style="text-align: left;">
>   Module Module1
> </p>
> 
> <p style="text-align: left;">
>   Sub Main()
> </p>
> 
> <p style="text-align: left;">
>   Dim theSession As Session = Session.GetSession()<br /> Dim theUISession As UI = UI.GetUI
> </p>
> 
> <p style="text-align: left;">
>   Dim workPart As Part = theSession.Parts.Work
> </p>
> 
> <p style="text-align: left;">
>   Dim lw As ListingWindow = theSession.ListingWindow<br /> lw.Open()<br /> Dim markId1 As Session.UndoMarkId<br /> markId1 = theSession.SetUndoMark(Session.MarkVisibility.Visible, &#8220;journal&#8221;)
> </p>
> 
> <p style="text-align: left;">
>   &#8216;change excelFileName to meet your needs<br /> Const excelFileName As String = &#8220;E:\Book1.xlsm&#8221;<br /> Dim row As Long = 1<br /> Dim column As Long = 1
> </p>
> 
> <p style="text-align: left;">
>   &#8216;create Excel object<br /> Dim objExcel = CreateObject(&#8220;Excel.Application&#8221;)<br /> If objExcel Is Nothing Then<br /> theUISession.NXMessageBox.Show(&#8220;Error&#8221;, NXMessageBox.DialogType.Error, &#8220;Could not start Excel, journal exiting&#8221;)<br /> theSession.UndoToMark(markId1, &#8220;journal&#8221;)<br /> Exit Sub
> </p>
> 
> <p style="text-align: left;">
>   End If
> </p>
> 
> <p style="text-align: left;">
>   &#8216;open Excel file<br /> Dim objWorkbook = objExcel.Workbooks.Open(excelFileName)<br /> If objWorkbook Is Nothing Then<br /> theUISession.NXMessageBox.Show(&#8220;Error&#8221;, NXMessageBox.DialogType.Error, &#8220;Could not open Excel file: &#8221; & excelFileName &                                                                                        ControlChars.NewLine & &#8220;journal exiting.&#8221;)<br /> theSession.UndoToMark(markId1, &#8220;journal&#8221;)<br /> Exit Sub<br /> End If
> </p>
> 
> <p style="text-align: left;">
>   objExcel.visible = True
> </p>
> 
> <p style="text-align: left;">
>   objExcel.Cells(row, 1) = workPart.FullPath
> </p>
> 
> <p style="text-align: left;">
>   For Each myDimension As Annotations.Dimension In workPart.Dimensions<br /> row += 1<br /> myDimension.GetDimensionText(myDimText, myDimDualText)<br /> objExcel.Cells(row, column) = myDimension.GetType.ToString<br /> objExcel.Cells(row, column+1) = myDimText(0)<br /> Next
> </p>
> 
> <p style="text-align: left;">
>   &#8216;objExcel.Quit()<br /> objWorkbook = Nothing<br /> objExcel = Nothing
> </p>
> 
> <p style="text-align: left;">
>   lw.Close()<br /> End Sub
> </p>