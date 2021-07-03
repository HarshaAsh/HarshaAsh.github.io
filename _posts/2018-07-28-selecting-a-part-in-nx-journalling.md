---
id: 360
title: Selecting a part in NX Journaling
date: 2018-07-28T17:09:25+05:30
author: Achyuthuni Sri Harsha
layout: post
guid: https://www.harshaash.com/?p=360
permalink: /selecting-a-part-in-nx-journalling/
categories:
  - NX Journalling
tags:
  - journaling
  - NX
---
This blog post is the first part of  <a href="https://www.harshaash.com/extracting-data-from-mechanical-models/" target="_blank" rel="noopener">3 part series on NX Journaling</a>

The aim of this blog post is to select a part.

&nbsp;

Before writing codes for journals, it&#8217;s easier to create a journal and then look at its code.

In NX 10.0, start recording a journal from tools -> journal

<img loading="lazy" class="size-medium wp-image-372 aligncenter" src="https://www.harshaash.com/wp-content/uploads/2018/07/nx-300x207.jpg" alt="" width="300" height="207" srcset="https://www.harshaash.com/wp-content/uploads/2018/07/nx-300x207.jpg 300w, https://www.harshaash.com/wp-content/uploads/2018/07/nx-768x529.jpg 768w, https://www.harshaash.com/wp-content/uploads/2018/07/nx.jpg 966w" sizes="(max-width: 300px) 100vw, 300px" /> 

Do the operations that you want to repeat, and stop the recording of the journal from tools -> journal

Look at the code created from the operations at tools -> journal -> edit

The code might look like this: (Visual basic code)

> <pre>' NX 10.0.0.24
' Journal created by Achyuthuni on Sun Jul 08 14:29:00 2018 India Standard Time
'
Option Strict Off
Imports System
Imports NXOpen

Module NXJournal
Sub Main (ByVal args() As String)

Dim theSession As NXOpen.Session = NXOpen.Session.GetSession()
Dim workPart As NXOpen.Part = theSession.Parts.Work

Dim displayPart As NXOpen.Part = theSession.Parts.Display

' ----------------------------------------------
' Menu: File-&gt;Show Dimensions
' ----------------------------------------------
Dim markId1 As NXOpen.Session.UndoMarkId
markId1 = theSession.SetUndoMark(NXOpen.Session.MarkVisibility.Visible, "Show Dimensions")

Dim extrude1 As NXOpen.Features.Extrude = CType(workPart.Features.FindObject("EXTRUDE(2)"), NXOpen.Features.Extrude)

extrude1.ShowDimensions()

Dim nErrs1 As Integer
nErrs1 = theSession.UpdateManager.DoUpdate(markId1)

' ----------------------------------------------
' Menu: Tools-&gt;Journal-&gt;Stop Recording
' ----------------------------------------------

End Sub
End Module</pre>

<a href="http://nxjournaling.com/content/beginning-journaling-using-nx-journal" target="_blank" rel="noopener">This article</a> helps in understanding more about understanding what each line of the code does, do read it if the above lines of code boggles you.

Our aim now is to modify this code to let user select the part that he requires, and to display its name in a popup window.

A listing window is a window like a popup which we are using to display dimensions.

getSelectedObject is a function that gets the selected object. This example aslo demonstrates how to write functions in VB.

Once the part is selected, its name and type are selected in the Listing window.

> <pre>' NX 10.0.0.24 
' Journal created by Achyuthuni on Sun Jul 08 14:29:00 2018 India Standard Time 
'
Option Strict Off
Imports System
Imports NXOpen
Imports NXOpen.UF

Module NXJournal
Sub Main

Dim theSession As Session = Session.GetSession()
Dim workPart As Part = theSession.Parts.Work
Dim displayPart As Part = theSession.Parts.Display
Dim lw As ListingWindow = theSession.ListingWindow
Dim mySelectedObject As NXObject

lw.Open
   mySelectedObject = getSelectedObject
   'these are the selections
   lw.WriteLine("Object Tag: " & mySelectedObject.Tag)
   lw.WriteLine("Object Type: " & mySelectedObject.GetType.ToString)
   lw.WriteLine("")
lw.Close

End Sub

Public Function getSelectedObject() as NXObject
   Dim returnSelectedObject As NXObject ' Ut: War daov rMIcrosoft COllection
   SelectAnObject("Please select an object", returnSelectedObject)
   Return returnSelectedObject
End Function

Function SelectAnObject(prompt As String, _
   ByRef selObj As NXObject) As Selection.Response

   Dim theUI As UI = UI.GetUI
   Dim cursor As Point3d
   Dim typeArray() As Selection.SelectionType = _
                      { Selection.SelectionType.All, _
                        Selection.SelectionType.Faces, _
                        Selection.SelectionType.Edges, _
                        Selection.SelectionType.Features }

    Dim resp As Selection.Response = theUI.SelectionManager.SelectObject( _
                                     prompt, "Selection", _
                                     Selection.SelectionScope.AnyInAssembly, _
                                     False, typeArray, selobj, cursor )

    If resp = Selection.Response.ObjectSelected Or _
        resp = Selection.Response.ObjectSelectedByName Then
        Return Selection.Response.Ok
    Else
        Return Selection.Response.Cancel
    End If

 End Function

End Module</pre>

The above code can also be found at <https://github.com/HarshaAsh/NXBasics>