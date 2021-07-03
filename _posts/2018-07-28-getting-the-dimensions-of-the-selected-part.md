---
id: 363
title: Getting the dimensions of the selected Part
date: 2018-07-28T17:24:55+05:30
author: Achyuthuni Sri Harsha
layout: post
guid: https://www.harshaash.com/?p=363
permalink: /getting-the-dimensions-of-the-selected-part/
categories:
  - NX Journalling
tags:
  - dimensions
  - journaling
  - NX
  - VB
---
This blog is the second part of a [3 part series on NX journalling](https://www.harshaash.com/extracting-data-from-mechanical-models/)

The aim of this blog post is to display dimensions of a part

Part dimensions will be stored in workPart.Dimensions and can be displayed on a listing window.

Continuing from the previous post, we could write the following program

> <p style="text-align: left;">
>   Imports System<br /> Imports NXOpen
> </p>
> 
> <p style="text-align: left;">
>   Module NXJournal<br /> Sub Main (ByVal args() As String)
> </p>
> 
> <p style="text-align: left;">
>   Dim theSession As NXOpen.Session = NXOpen.Session.GetSession()<br /> Dim workPart As NXOpen.Part = theSession.Parts.Work
> </p>
> 
> <p style="text-align: left;">
>   Dim displayPart As NXOpen.Part = theSession.Parts.Display<br /> Dim markId1 As NXOpen.Session.UndoMarkId
> </p>
> 
> <p style="text-align: left;">
>   markId1 = theSession.SetUndoMark(NXOpen.Session.MarkVisibility.Visible, &#8220;Show Dimensions&#8221;)
> </p>
> 
> <p style="text-align: left;">
>   Dim lw As ListingWindow = theSession.ListingWindow
> </p>
> 
> <p style="text-align: left;">
>   Dim extrude1 As NXOpen.Features.Extrude = CType(workPart.Features.FindObject(&#8220;EXTRUDE(2)&#8221;), NXOpen.Features.Extrude)
> </p>
> 
> <p style="text-align: left;">
>   <strong>extrude1.ShowDimensions()</strong>
> </p>
> 
> <p style="text-align: left;">
>   <strong>For Each tempDim As Annotations.Dimension In workPart.Dimensions</strong><br /> <strong>            Dim myDimText() As String</strong><br /> <strong>            Dim myDimDualText() As String</strong><br /> <strong>            lw.WriteLine(&#8220;dimension type is &#8221; & tempDim.GetType.ToString)</strong><br /> <strong>            tempDim.GetDimensionText(myDimText, myDimDualText)</strong><br /> <strong>            lw.WriteLine(&#8220;dimension value is &#8221; & myDimText(0))</strong><br /> <strong>        Next</strong>
> </p>
> 
> <p style="text-align: left;">
>   Dim nErrs1 As Integer<br /> nErrs1 = theSession.UpdateManager.DoUpdate(markId1)
> </p>
> 
> <p style="text-align: left;">
>   End Sub<br /> End Module
> </p>

The above code can also be found at <https://github.com/HarshaAsh/NXBasics>