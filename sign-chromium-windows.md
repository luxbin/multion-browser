Typical path to signtool on Windows 10 or 11.

32 bit: "C:\Program Files (x86)\Windows Kits\10\bin\10.0.22000.0\x86\signtool.exe"

64 bit: "C:\Program Files (x86)\Windows Kits\10\bin\10.0.22000.0\x64\signtool.exe"

(10.0.22000.0 or any version folder)

You can use x86 or x64 signtool.exe

Open the Command Prompt with administrative privileges

```
signtool sign /f "C:\path\to\certificate.pfx" /p "your_certificate_password" /tr "http:/rfc3161timestamp.globalsign.com/advanced" /td SHA256 /fd SHA256 "C:\path\to\your\app.exe"
```