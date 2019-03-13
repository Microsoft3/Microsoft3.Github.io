---
layout: post
title: Pure PowerShell Post–Going Through Setting a Basic PowerShell Progress Bar–For future reference when I’ll need to use/demo a progress bar …
date: 2017-10-29 21:16
author: sammykrosoft
comments: true
categories: [Uncategorized]
---
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEPS FOR USING A PROGRESS BAR</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#NOTE: You can copy paste that whole post to an ISE or a NOTEPAD and save it as a .ps1 script - the explanations are put in comments for that purpose :-)</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEP 1 - Get your main objects collection you're going to browse and for which you wish to monitor progression - it can be a Get-Item, or an Import-CSV or a manual list for example - $Mylist = "Server1", "Server2", "Server3", "Server4"</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span style="font-family: Lucida Console"><span><span style="color: #ff4500"><span style="font-size: 9pt">$MyListOfObjectsToProcess</span></span></span><span><span style="font-size: 9pt"><span style="color: #000000"> </span><span><span style="color: #d3d3d3">=</span></span><span style="color: #000000"> </span><span><span style="color: #db7093">"Server1"</span></span><span><span style="color: #d3d3d3">,</span></span><span><span style="color: #db7093">"Server2"</span></span><span><span style="color: #d3d3d3">,</span></span><span><span style="color: #db7093">"Server3"</span></span><span><span style="color: #d3d3d3">,</span></span><span><span style="color: #db7093">"Server4"</span></span><span><span style="color: #d3d3d3">,</span></span><span><span style="color: #db7093">"Server5"</span></span><span><span style="color: #d3d3d3">,</span></span></span><span><span style="color: #db7093;font-size: 9pt">"Server6"</span></span><span></span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEP 2 - We need to know how much<span>  </span>items we will have to process (to calculate the % done later on) </span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span style="font-family: Lucida Console"><span><span style="color: #ff4500"><span style="font-size: 9pt">$TotalItems</span></span></span><span><span style="font-size: 9pt"><span style="color: #000000"> </span><span><span style="color: #d3d3d3">=</span></span><span style="color: #000000"> </span><span><span style="color: #ff4500">$MyListOfObjectsToProcess</span></span><span><span style="color: #d3d3d3">.</span></span></span><span><span style="color: #f5f5f5;font-size: 9pt">count</span></span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEP 3 - We need to initialize a counter to know what % is done</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span style="font-family: Lucida Console"><span><span style="color: #ff4500"><span style="font-size: 9pt">$Counter</span></span></span><span><span style="font-size: 9pt"><span style="color: #000000"> </span><span><span style="color: #d3d3d3">=</span></span><span style="color: #000000"> </span></span><span><span style="color: #ffe4c4;font-size: 9pt">0</span></span><span></span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEP 4 - Process each item (Foreach $Item) of your List Of Objects To Process (in $MyListOfObjectsToProcess)</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span style="font-family: Lucida Console"><span><span style="color: #e0ffff"><span style="font-size: 9pt">Foreach</span></span></span><span><span style="font-size: 9pt"><span style="color: #000000"> </span><span><span style="color: #f5f5f5">(</span></span><span><span style="color: #ff4500">$Item</span></span><span style="color: #000000"> </span><span><span style="color: #e0ffff">in</span></span><span style="color: #000000"> </span><span><span style="color: #ff4500">$MyListOfObjectsToProcess</span></span><span><span style="color: #f5f5f5">)</span></span><span style="color: #000000"> </span></span><span><span style="color: #f5f5f5;font-size: 9pt">{</span></span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEP 5 - We increment the counter</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span><span style="color: #98fb98;font-size: 9pt">#<span>  </span>NOTE 1 : if we initialize the counter to $Counter = 1, then we can increment the counter at the end of the Foreach block - in this example we initialized the counter to $Counter = 0 then we increment it right away to go to "1" first ... </span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span><span style="color: #98fb98;font-size: 9pt">#<span>  </span>NOTE 2 :Developpers like to start at "0" so usually you'll see counters increment at the end of ForEach-like loops - I'm just not following the sheep here, just because I'm French :-p</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span style="font-size: 9pt"><span><span style="color: #ff4500">$Counter</span></span></span><span><span style="color: #d3d3d3;font-size: 9pt">++</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#STEP 6 - Here is the core : Write-Progress - it comes with 3 mandatory properties : ACTIVITY, STATUS and PERCENTCOMPLETE</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span><span style="color: #98fb98;font-size: 9pt">#<span>  </span>ACTIVITY is the title of the progress bar</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span><span style="color: #98fb98;font-size: 9pt">#<span>  </span>STATUS is to show on screen which element it is currently processing (Processing item #2 of #20000)</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span><span style="color: #98fb98;font-size: 9pt">#<span>  </span>PERCENTCOMPLETE is the progress bar itself and it has to be a percentage (hence the $($Counter / $TotalRecipients * 100) as we calculate the percentage on the fly...</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span style="font-size: 9pt"><span><span style="color: #e0ffff">Write-Progress</span></span><span style="color: #000000"> </span><span><span style="color: #ffe4b5">-Activity</span></span><span style="color: #000000"> </span><span><span style="color: #db7093">"Processing Items"</span></span><span style="color: #000000"> </span><span><span style="color: #ffe4b5">-Status</span></span><span style="color: #000000"> </span><span><span style="color: #db7093">"Item </span></span><span><span style="color: #ff4500">$Counter</span></span><span><span style="color: #db7093"> of </span></span><span><span style="color: #ff4500">$TotalItems</span></span><span><span style="color: #db7093">"</span></span><span style="color: #000000"> </span><span><span style="color: #ffe4b5">-PercentComplete</span></span><span style="color: #000000"> </span><span><span style="color: #f5f5f5">$(</span></span><span><span style="color: #ff4500">$Counter</span></span><span style="color: #000000"> </span><span><span style="color: #d3d3d3">/</span></span><span style="color: #000000"> </span><span><span style="color: #ff4500">$TotalItems</span></span><span style="color: #000000"> </span><span><span style="color: #d3d3d3">*</span></span><span style="color: #000000"> </span><span><span style="color: #ffe4c4">100</span></span></span><span><span style="color: #f5f5f5;font-size: 9pt">)</span></span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#YOUR ROUTINE - Here whatever you want to process on each $Item - that doesn't change anything to the Write-Progress, apart from the time it takes for the progress bar to go to the next % done...</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#<span>  </span>In the below example it's just sleeping for 1 second, then outputting each $Item we're processing for the Demo purposes ...</span></span></span><span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span style="font-size: 9pt"><span><span style="color: #e0ffff">sleep</span></span><span style="color: #000000"> </span></span><span><span style="color: #ffe4c4;font-size: 9pt">1</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span><span style="color: #000000"><span style="font-size: 9pt">    </span></span></span><span style="font-size: 9pt"><span><span style="color: #e0ffff">Write-Host</span></span><span style="color: #000000"> </span></span><span><span style="color: #ff4500;font-size: 9pt">$Item</span></span></span><span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt">}</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #f5f5f5;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">&lt;# Fore more information visit:</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">Powershell progress bar basics :</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">https://technet.microsoft.com/en-us/library/ff730943.aspx</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">A little bit more with Write-Progress:</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">https://technet.microsoft.com/en-us/library/2008.03.powershell.aspx</span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt"> </span></span></span></p>
<p class="MsoNormal" style="background: #012456;margin: 0cm 0cm 0pt;line-height: normal"><span><span style="font-family: Lucida Console"><span style="color: #98fb98;font-size: 9pt">#&gt; </span></span></span></p>
<p class="MsoNormal" style="margin: 0cm 0cm 8pt;line-height: 12pt"><span style="font-family: Calibri"><span style="color: #000000;font-size: 11pt"> </span></span></p>