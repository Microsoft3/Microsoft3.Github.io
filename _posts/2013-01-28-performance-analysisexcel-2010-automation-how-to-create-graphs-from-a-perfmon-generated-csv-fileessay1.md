---
layout: post
title: Performance Analysis–Excel (2010) automation : how to create graphs from a Perfmon-generated CSV file–Essay#1
date: 2013-01-28 19:30
author: sammykrosoft
comments: true
categories: [Uncategorized]
---
<p>&#160;</p>  <p>Hi all,</p>  <p>Today I’m concentrating my efforts into generating graphs as painless as possible for many data collected on Exchange servers. I’ll start by generating graphs from the two following counters which give an idea of the load of the servers:</p>  <p>- Active User Count</p>  <p>- RPC Operations/sec</p>  <p>The first step (Essay#1) is to generate as quickly as possible a nice graph to display the trend for these counters.</p>  <p>The second step (Essay#2) will be to generate quickly also graphs from a bunch of files located on a folder.</p>  <p>The third step (Essay#3) will be to quickly generate these graphs on a separate Excel spreadsheet, or even better on a Word document to start a report</p>  <p>the fourth step (Essay #4) will then be to generate the most significant graphs to generate a report that will enable a good graphical performance analysis of many servers at a time, simply using Excel and Word.</p>  <p>&#160;</p>  <p>First you need to collect Perfmon data and configure the Perfmon data collector to dump statistics on .CSV files. You can also chose to convert existing BLG files to .CSV files using RELOG for example … or loading .BLG files onto a Perfmon console, and export the data on .CSV files … many ways to do this, but it’s not the purpose of this post.</p>  <p>&#160;</p>  <p>Second, we will then generate our graph with the above mentioned two counters (as a start of my live project). </p>  <p>You have to open Excel 2010, show the “Developer” tab, and copy the following code :</p>  <p><font face="Courier New">Sub Macro_Search_Active_User()</font></p>  <p>   <br /><font face="Courier New"><em>'NAME the first column which is the timeline column       <br /></em>Range(&quot;A:A&quot;).Name = &quot;Time_Line&quot;</font></p>  <p><font face="Courier New"><em>'FIND the column showing the number of active user count       <br /></em>&#160;&#160;&#160; Cells.Find(What:=&quot;Active User Count&quot;, After:=ActiveCell, LookIn:=xlFormulas, _      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; LookAt:=xlPart, SearchOrder:=xlByRows, SearchDirection:=xlNext, _      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; MatchCase:=False, SearchFormat:=False).Select      <br /><em>'NAME the column just found       <br /></em>Range(Selection, Selection.End(xlDown)).Name = &quot;Active_User_Count&quot;</font></p>  <p><font face="Courier New"><em>'FIND the column showing the RPC activity       <br /></em>&#160;&#160;&#160; Cells.Find(What:=&quot;RPC Operations/sec&quot;, After:=ActiveCell, LookIn:=xlFormulas, _      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; LookAt:=xlPart, SearchOrder:=xlByRows, SearchDirection:=xlNext, _      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; MatchCase:=False, SearchFormat:=False).Select      <br /><em>'NAME the column just found</em>      <br />Range(Selection, Selection.End(xlDown)).Name = &quot;RPC_Ops_Per_Sec&quot;</font></p>  <p><font face="Courier New"><em>'SELECT then all these 3 colums</em>      <br />Range(&quot;Time_Line, Active_User_Count, RPC_Ops_Per_Sec&quot;).Select      <br />Range(&quot;A1&quot;).Activate</font></p>  <p><font face="Courier New"><em>'GENERATE the Excel graph       <br /></em>ActiveSheet.Shapes.AddChart2(227, xlLine).Select      <br />ActiveChart.SetSourceData Source:=Range(&quot;Time_Line, Active_User_Count, RPC_Ops_Per_Sec&quot;)      <br /><em>'NAME the graph to easily retrieve it on other code lines       <br /></em>ActiveChart.Parent.Name = &quot;ActiveUsersAndRPCOps&quot;</font></p>  <p><font face="Courier New"><em>'This step is optional : DELETE the X axe label - &quot;xlCategory&quot; (or find an equivalent function to deactivate it) – because you may want to keep the X-axe time data</em>      <br />ActiveChart.Axes(xlCategory).Select      <br />Selection.Delete</font></p>  <p><font face="Courier New"><em>' Add a secondary Axe for one of the data series(no matter which one)</em>      <br /><em>' .. Select series nb 1</em>      <br />ActiveChart.FullSeriesCollection(1).Select      <br /><em>' .. add data as a secondart axe</em>      <br />ActiveChart.FullSeriesCollection(1).AxisGroup = 2      <br /><em>' .. Color selected collection to in RGB(xxx,xxx,xxx) </em>with xxx btw 0 and 255      <br />&#160;&#160;&#160; With Selection.Format.Line      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Visible = msoTrue      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .ForeColor.RGB = RGB(255, 0, 0)      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Transparency = 0      <br />&#160;&#160;&#160; End With      <br /><em>' .. Color the axis linked to the secondary collection into the same color       <br />' ... Select the secondary axe first        <br /></em>ActiveChart.Axes(xlValue, xlSecondary).Select      <br /><em>' ... then set the selection properties : line visible, color and not transparent ...       <br /></em>&#160;&#160;&#160; With Selection.Format.Line      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Visible = msoTrue      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .ForeColor.RGB = RGB(255, 0, 0)      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Transparency = 0      <br />&#160;&#160;&#160; End With      <br />&#160;&#160;&#160; ActiveChart.Axes(xlValue, xlSecondary).Select      <br />&#160;&#160;&#160; With Selection.TickLabels.Font      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Color = RGB(255, 0, 0)      <br />&#160;&#160;&#160; End With</font></p>  <p>   <br /><font face="Courier New"><em>'. Same SELECTing and FORMATting the second data collection and axe       <br /></em>ActiveChart.FullSeriesCollection(2).Select      <br />&#160;&#160;&#160; With Selection.Format.Line      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Visible = msoTrue      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .ForeColor.RGB = RGB(0, 130, 0)      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Transparency = 0      <br />&#160;&#160;&#160; End With      <br />ActiveChart.Axes(xlValue).Select      <br />&#160;&#160;&#160; With Selection.Format.Line      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Visible = msoTrue      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .ForeColor.RGB = RGB(0, 130, 0)      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .Transparency = 0      <br />&#160;&#160;&#160; End With</font></p>  <p>   <br /><font face="Courier New"><em>'Finally, delete the title       <br /></em>&#160;&#160;&#160; ActiveChart.ChartTitle.Select      <br />&#160;&#160;&#160; Selection.Delete</font></p>  <p><font face="Courier New">End Sub</font></p>  <p>&#160;</p>  <p>Execute the macro and you’ll instantly have the following type of graph:</p>  <p><a href="https://msdnshared.blob.core.windows.net/media/TNBlogsFS/prod.evol.blogs.technet.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/73/61/metablogapi/6366.image_4.png" original-url="http://blogs.technet.com/cfs-file.ashx/__key/communityserver-blogs-components-weblogfiles/00-00-00-73-61-metablogapi/6366.image_5F00_4.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="https://msdnshared.blob.core.windows.net/media/TNBlogsFS/prod.evol.blogs.technet.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/73/61/metablogapi/1563.image_thumb_1.png" original-url="http://blogs.technet.com/cfs-file.ashx/__key/communityserver-blogs-components-weblogfiles/00-00-00-73-61-metablogapi/1563.image_5F00_thumb_5F00_1.png" width="569" height="343" /></a></p>    <p>&#160;</p>  <p>Next I’ll try (and succeed hopefully) to generate the above graph type for many CSV Perfmon files stored in a directory.</p>