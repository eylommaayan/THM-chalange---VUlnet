# THM-chalange---VUlnet




## שלב 1: סריקת פורטים וזיהוי שירותים (Service Enumeration)

### **תיאור (Description)**
השלב הראשון בתהליך הפריצה הוא זיהוי "שטח התקיפה" (Attack Surface) של מכונת היעד. לשם כך, בוצעה סריקה באמצעות כלי ה-**Nmap** כדי לזהות פורטים פתוחים, שירותים פעילים וגרסאות תוכנה הרצות עליהם.

### **ביצוע (Execution)**
הפקודה שהורצה:
`nmap 10.114.132.121 -sCV`

* **-sC**: הרצת סקריפטים כברירת מחדל של Nmap (לאיתור חולשות בסיסיות).
* **-sV**: זיהוי גרסאות השירותים (Version Detection).

### **ממצאים (Findings)**
הסריקה העלתה שני פורטים פתוחים עיקריים:

| פורט (Port) | מצב (State) | שירות (Service) | גרסה (Version) | הערות |
| :--- | :--- | :--- | :--- | :--- |
| **22** | Open | **SSH** | OpenSSH 7.6p1 | שירות לחיבור מרחוק (Ubuntu Linux). |
| **80** | Open | **HTTP** | Apache httpd 2.4.29 | שרת אינטרנט המציג אתר עם הכותרת "VulnNet". |

### **ניתוח (Analysis & Insights)**
1.  **פורט 80 (HTTP):** זהו וקטור התקיפה המרכזי בשלב זה. מכיוון שהסריקה זיהתה כותרת ספציפית ("VulnNet"), עולה החשד שהשרת עושה שימוש ב-Virtual Hosting, מה שדורש מאיתנו לבצע מיפוי DNS ידני (עריכת קובץ ה-Hosts) כדי לגשת לתוכן המלא.
2.  **פורט 22 (SSH):** גרסת ה-OpenSSH מעודכנת יחסית ואינה פגיעה לחולשות ידועות המאפשרות כניסה ללא פרטי גישה. לכן, פורט זה ישמש אותנו רק לאחר שנשיג שם משתמש וסיסמה/מפתח דרך האתר.

---

<img width="982" height="422" alt="image" src="https://github.com/user-attachments/assets/038f575a-4636-41ac-a8a3-6e88c6f149e8" />


שלב 2: הגדרת מיפוי DNS מקומי (Local DNS Resolution)
תיאור הפעולה (Description)
לאחר זיהוי שרת HTTP פעיל בפורט 80, בוצע עדכון של קובץ המארחים המקומי (/etc/hosts). פעולה זו נועדה לאפשר למערכת ה-Kali לזהות את הכתובת vulnnet.thm ולהפנות אותה לכתובת ה-IP של היעד. הגדרה זו קריטית במקרים של Virtual Hosting, שבהם השרת מציג תוכן שונה בהתאם לשם הדומיין המבוקש ב-HTTP Header.

שלבי ביצוע (Execution Steps)
פתיחת עורך הקבצים בהרשאות מנהל:
בוצעה גישה לקובץ הקונפיגורציה באמצעות הפקודה:
<img width="503" height="164" alt="image" src="https://github.com/user-attachments/assets/187cc481-1e73-4d7d-a1a9-8c367584b148" />


Bash
sudo nano /etc/hosts
הוספת רשומת ה-Static IP:
בסוף הקובץ התווספה השורה הבאה המקשרת בין ה-IP לדומיין:

Plaintext
10.114.132.121  vulnnet.thm
<img width="852" height="552" alt="image" src="https://github.com/user-attachments/assets/de5707d4-9f96-478d-af50-f673bf4bbb15" />

שמירה ועדכון:
הקובץ נשמר (Ctrl+O) ונסגר (Ctrl+X) כדי להחיל את השינויים באופן מיידי במערכת.

אימות (Verification)
בוצע ניסיון גלישה באמצעות הדפדפן לכתובת http://vulnnet.thm. האתר נטען בהצלחה, מה שמאשר כי השרת מוגדר להגיב לשם דומיין זה וכי ניתן להמשיך לשלב סריקת הספריות וה-Subdomains.





<img width="790" height="600" alt="image" src="https://github.com/user-attachments/assets/65802b85-530e-4578-a0cf-c5652e96176c" />


<img width="1093" height="904" alt="image" src="https://github.com/user-attachments/assets/a6e3cd77-7312-49d7-a2c1-5149abd7aa83" />

