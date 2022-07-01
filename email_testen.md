Um mail in einer App zu testen:
https://github.com/rnwood/smtp4dev/wiki/Installation

Anzufangen:
smtp4dev

Man muss die Emails von name@localhost schicken. Dann wird man die Emails in localhost:5000 sehen

Zu testen ob es funktioniert (PowerShell script):
Send-MailMessage -SmtpServer localhost -Subject "Hello World" -Body "Hello World" -From "admin@localhost" -To "user@asdfasdf"