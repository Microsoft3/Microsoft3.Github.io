---
layout: post
title: Outlook antivirus exclusions (reminder)
date: 2014-06-20 09:59
author: sammykrosoft
comments: true
categories: [Uncategorized]
---
<p><font size="2">&nbsp;</font><font size="2"></font><p><font size="2">Hi all,</font></p><font size="2"></font><p>&nbsp;</p><p><font size="2">Here are a few examples of which issues you can expect as well if some software are preventing access, even temporarily, to Outlook Cache mode files:</font></p><p><font size="2"></font></p><p><font size="2">- a manager with many secretaries who have delegations rights on this manager&rsquo;s mailbox, and who organize meetings on behalf of the boss &ndash; inconsistencies will arise overtime on meeting organizer and meeting attendees, which can be directly related to AV scanning Outlook cache files (OST, OST.tmp,xml,&hellip;) &ndash; or any other software who can have a handle on these files.</font></p><p><font size="2">- desktop load from other application also plays a role in the frequency the above mentioned issues appearance, as applications like Outlook may be slower to process elements and will need more time handling OST, ost.tmp, profile_name.xml, .oab, etc&hellip; files and need more constant access to these =&gt; if the antivirus are handling these files at the same time, chances to have issues are multiplied.</font></p><p><font size="2">- Outlook in cache mode is freezing as the application is trying to access its OST or other cache related files (as well as PST files sometimes &ldquo;hooked&rdquo; by AV software &ndash; remember not to put PST files on network shares or mapped drives) &ndash; Outlook in cache mode will NEVER freeze, unless the mentionned case on this example, OR any piece of online mode that is used on the user profile (Example: access to shared folders or mailboxes for which cache mode is not configured &ndash; this is a check box on the Outlook options for the current profile, or the OAB is not downloaded, then Outlook uses Online mode Address Book for example)</font></p><p><font size="2"></font></p><p><font size="2">Note that frequency of these also increases as certain conditions of daily utilizations are met.The above examples of issues can be hard to reproduce on a lab.</font></p><p><font size="2"></font></p><p><font size="2"></font></p><p><font size="2">I&rsquo;m adding some more information regarding Outlook latency causes that can be on the Desktop side.</font></p><p>&nbsp;</p><p><strong><u><font size="4">&gt; Outlook 2007/2010 &ndash; More precisions about Antivirus exclusions and things that can slow down your messaging client in general</font></u></strong></p><p><a href="http://blogs.technet.com/b/samdrey/archive/2012/10/10/outlook-2007-2010-some-basic-advice-if-you-experience-startup-latencies.aspx">http://blogs.technet.com/b/samdrey/archive/2012/10/10/outlook-2007-2010-some-basic-advice-if-you-experience-startup-latencies.aspx</a></p><p>&nbsp;</p><p>&nbsp; </p><p><strong><u><font size="4">&gt; Plan antivirus scanning for Outlook 2010</font></u></strong></p><p><a href="http://technet.microsoft.com/en-us/library/hh550032(v=office.14).aspx">http://technet.microsoft.com/en-us/library/hh550032(v=office.14).aspx</a></p><p><strong><u><em>Quotes:</em></u></strong></p><p><font size="2"><em>- </em><em>We recommend that you turn off scanning of the following Microsoft Outlook files:</em></font></p><ul>   <li>     <p><em><font size="2">*.oab (Outlook address book files)</font></em></p>      <p><em><font size="2">%userprofile%AppDataLocalMicrosoftOutlookOffline Address Books&lt;guid&gt;</font></em></p>   </li>    <li>     <p><em><font size="2">*.srs (send/receive settings files)</font></em></p>      <p><em><font size="2">%userprofile%AppDataRoamingMicrosoftOutlook</font></em></p>   </li>    <li>     <p><em><font size="2">Navigation pane settings file profile_name.xml files</font></em></p>      <p><em><font size="2">%userprofile%AppDataRoamingMicrosoftOutlook&lt;profile name&gt;.xml</font></em></p>      <p><em><font size="2">where &lt;profile name&gt; is the name of the Outlook messaging profile, as shown in the Control Panel, Mail applet.</font></em></p>   </li>    <li>     <p><em><font size="2">outlprnt (print styles)</font></em></p>      <p><em><font size="2">%userprofile%AppDataRoamingMicrosoftOutlook</font></em></p>   </li> </ul><font size="2"></font><p><i><font size="2">-&nbsp; If you use antivirus software to perform file-level scanning [Outlook files], while Outlook is in use, data corruption issues might result.</font></i></p><font size="2"></font><p><i><font size="2">- We we do not recommend that you scan *.pst, *.ost, and other Outlook files directly. Instead, we recommend that you scan email message attachments on the email server and on the Outlook client computer.</font></i></p><p><em></em></p><p>&nbsp;&nbsp;&nbsp; </p><p><u><font size="4"><strong>&gt; How to troubleshoot performance issues in Outlook 2010</strong></font></u></p><p><a title="http://support2.microsoft.com/kb/2695805" href="http://support2.microsoft.com/kb/2695805">http://support2.microsoft.com/kb/2695805</a></p><p><strong><u><em>Quote:</em></u></strong></p><p><em><font size="2">- The performance issues may be caused by one or more of the following:&nbsp; </font></em></p><ul>   <li><em><font size="2">Insufficient computer specifications </font></em></li>    <li><em><font size="2">Absence of the latest service pack for Outlook 2010 </font></em></li>    <li><em><font size="2">Large Personal Folders files (.pst) or Offline Folder files (.ost) </font></em></li>    <li><em><font size="2">Outlook .ost files or .pst files that are stored on a drive with insufficient write performance </font></em></li>    <li><em><font size="2">Third-party add-ins </font></em></li>    <li><em><font size="2">Gadgets that access Outlook data (Windows Vista only) </font></em></li>    <li><em><font size="2">Microsoft Office Communicator integration </font></em></li>    <li><em><font size="2">Antivirus software interaction </font></em></li>    <li><em><font size="2">Windows Desktop Search indexing </font></em></li>    <li><em><font size="2">Incomplete closure of .pst files or .ost files </font></em></li>    <li><em><font size="2">POP3 accounts on Windows Vista clients </font></em></li>    <li><em><font size="2">Many Really Simple Syndication (RSS) feeds </font></em></li>    <li><em><font size="2">To-Do Bar and Online mode with Exchange server </font></em></li>    <li><em><font size="2">Damaged Outlook messaging profile</font></em></li> </ul></p>
