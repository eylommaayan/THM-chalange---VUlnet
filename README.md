# THM-chalange---VUlnet




Step 2: Configure Local DNS Resolution
Description
During the Nmap scan, an HTTP server (port 80) running the VulnNet header was detected. Web servers often use Virtual Hosting, which means that the server will display different content or only allow access if it is addressed using a specific domain name and not just the IP address.

To simulate normal browsing and allow the browser and scanning tools (like Feroxbuster) to communicate with the server on its behalf, we need to update the /etc/hosts file.

Steps
Open the configuration file of the local system that manages domain names manually:

Bash
sudo nano /etc/hosts
Enter the system password (kali) to obtain administrator (Root) privileges.

Add a record that maps the target IP address to the requested domain name:

Plaintext
10.112.161.133 vulnnet.thm
Save the file and exit the editor.

Rationale
This ensures that any request to http://vulnnet.thm will be directed directly to the IP address of the machine on TryHackMe. Without this step, we may get a "404 Not Found" error or a default Apache page, as the server will not recognize that we are trying to reach the specific room website.



<img width="1093" height="904" alt="image" src="https://github.com/user-attachments/assets/a6e3cd77-7312-49d7-a2c1-5149abd7aa83" />


שלב 2: הגדרת מיפוי DNS מקומי (Local DNS Resolution)
תיאור (Description)
במהלך סריקת ה-Nmap זוהה שרת HTTP (פורט 80) המריץ את הכותרת VulnNet. לעיתים קרובות, שרתי אינטרנט משתמשים ב-Virtual Hosting, מה שאומר שהשרת יציג תוכן שונה או יאפשר גישה רק אם פונים אליו באמצעות שם דומיין ספציפי ולא רק דרך כתובת ה-IP.

כדי לדמות גלישה תקינה ולאפשר לדפדפן ולכלי הסריקה (כמו Feroxbuster) לתקשר עם השרת בשמו, עלינו לעדכן את קובץ ה-/etc/hosts.

פעולות לביצוע (Steps)
פתיחת קובץ הקונפיגורציה של המערכת המקומית המנהלת שמות דומיינים ידניים:

Bash
sudo nano /etc/hosts
הזנת סיסמת המערכת (kali) לשם קבלת הרשאות מנהל (Root).

הוספת רשומה המקשרת בין כתובת ה-IP של היעד לשם הדומיין המבוקש:

Plaintext
10.112.161.133   vulnnet.thm
שמירת הקובץ ויציאה מהעורך.

רציונל (Rationale)
פעולה זו מבטיחה שכל בקשה שנשלח לכתובת http://vulnnet.thm תופנה ישירות לכתובת ה-IP של המכונה ב-TryHackMe. ללא שלב זה, ייתכן שנקבל שגיאת "404 Not Found" או דף ברירת מחדל של Apache, מכיוון שהשרת לא יזהה שאנחנו מנסים להגיע לאתר הספציפי של החדר.
