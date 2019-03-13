---
layout: post
title: Exchange Server 2010 – If search fails after upgrading to SP3 (RU2 as well in this case)
date: 2013-09-03 07:50
author: sammykrosoft
comments: true
categories: [Uncategorized]
---
<p>&nbsp;<p>First, as my colleague Rhoderick wrote in a <a href="http://blogs.technet.com/b/mspfe/archive/2012/04/27/how-to-troubleshoot-issues-with-exchange-2010-search.aspx">nice and easy-to-read &ldquo;Troubleshooting Content Indexing&rdquo; article</a>, we can use the <b>Troubleshoot-CI.ps1</b> script to try detect other potential issues such as deadlocks (threads blocked and search is waiting on these to continue to index), corruption (not likely here as the state is &ldquo;Healthy&rdquo; for the indexes), stall (usually a one time issue that a restart of the Exchange Search service solves), backlog.</p><p>In case the above troubleshooter is not identifying any issues, we can proceed to the below steps.</p><p>&nbsp;</p><p>First, check that any File-Level anti-virus exclude the scan of any Exchange Index files (as well as DB files, and other Exchange files).</p><p>&nbsp;</p><p>Then, rebuild the symbolic links for each language that the SP may have striped out, and reset the index:</p><p>-&gt; Open Exchange Management Shell by right-clicking the shortcut and selecting &ldquo;Run as Administrator&rdquo;.</p><p>-&gt; Navigate to the Scripts folder from <b>Exchange</b> Management Shell.</p><p>-&gt; Run the command, ".Repair-ExchangeSearchSymlinks.ps1" and check that it is completing successfully.</p><p>-&gt; Run the command, ".ResetSearchIndex.ps1 -force "Mailbox Database" and check that it&rsquo;s completing successfully.</p><p>&nbsp;</p><p>Then disable TCP Chimney, RSS and NetDMA that may be a cause for this issue as well</p><p>-&gt; Open Command Prompt and run the following NetSH commands:</p><blockquote>   <p>Disable TCP Chimney (the functionnality to offload the network packet processing from the CPU to the Network Card)     <br> =&gt; netsh int tcp set global chimney=disabled </p>    <p>Disable RSS     <br> =&gt; netsh int tcp set global rss=disabled </p>    <p>Disable NetDMA (Network Direct Memory Access)     <br> =&gt; Opened Registry Editor and navigated to HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesTcpipParameters      <br> =&gt; Right click Parameters and add a new DWORD (32-bit) EnableTCPA and set the value to 0. </p> </blockquote><p>Information for TCP, RSS, NetDMA/EnableTCPA can be found on <a title="http://support.microsoft.com/kb/951037/en-us" href="http://support.microsoft.com/kb/951037/en-us">http://support.microsoft.com/kb/951037/en-us</a></p><p>&nbsp;</p><p>Optionnally, you can also disable IPV6 as well:   <br> =&gt; Open Registry Editor and navigate to HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesTcpipParameters    <br> =&gt; Right click Parameters and add a new DWORD (32-bit) DisabledComponents and set the value to 0xffffffff in Hexadecimal.</p><p>More information on <a title="http://technet.microsoft.com/en-us/network/cc987595.aspx" href="http://technet.microsoft.com/en-us/network/cc987595.aspx">http://technet.microsoft.com/en-us/network/cc987595.aspx</a></p><p>&nbsp;</p><p>&nbsp;</p><p>Finally, reboot the Exchange server to apply the above changes.</p><p>&nbsp;</p><p>I recommend you test this procedure on a Lab first to get familiar with it, and to validate it in your environment before implementing these into production.</p><p>&nbsp;</p><p>Sam.</p></p>
