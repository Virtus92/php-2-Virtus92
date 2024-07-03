# PHP 2 + CSS Frameworks Kompetenzcheck
**Erstelle ein kleines CRM-System (Customer Relation Management)**

**Ziel:**  
- Entwickle ein kleines Kundenverwaltungssystem für ein KMU (Klein- und Mittelunternehmen), das Überblick über seine KundInnendaten erhalten möchte.  
- Die eingetragenen KundInnen sollen in einer MYSQL Datenbank abgespeichert werden, man muss die Daten bearbeiten und sich eine Übersicht der Einträge anzeigen lassen können.  
- Nutze für die Verbindung zur Datenbank PDO.  

**Anforderungen:**  

Die Tabellen in der Datenbank sollen folgendermaßen aussehen:  
- users: user_id, name, email, password  
- customers: company_id, company_name, contact_person, phone, adress, created_by (welcher User hat den Eintrag erstellt), created_at(Erstelldatum), edited_at(Bearbeitungsdatum)  
- Relation: users 1 – n customers    

**Features:**  
- User-Registrierung  
- User-LogIn  
- Anlegen von NeukundInnen über ein Kontaktformular  
- Übersicht aller KundInnen  
- Möglichkeit jeden Eintrag zu bearbeiten & zu löschen  
- Eingeloggte User können alle Einträge im System sehen  
- ABER: Eingeloggte User können nur die Einträge bearbeiten bzw. löschen, die sie auch selbst erstellt haben. (Tipp: Das könnt ihr mit einer Session lösen).  

**Benutzeroberfläche**  
- Für die Benutzeroberfläche (GUI) verwendet bitte eines der CSS Frameworks aus dem Modul CSS Frameworks (Ja, so könnt ihr beide Kompetenzen miteinander abschließen 😉).   
- Gestaltet das Kundenverwaltungssystem benutzerfreundlich! (gutes Userfeedback bei den Kontaktformularen, deutliche Hinweise, wenn etwas nicht geklappt hat, etc.)  
- Achtet beim Styling auf gute Lesbarkeit, Farben, die nicht ablenken etc.  
- Denkt auch an die Responsive Gestaltung des Tools & passt euer CSS dementsprechend an.  
---

EN:  

**Objective:**  

Develop a small customer management system for a SME (Small and Medium-sized Enterprise) that wants to have an overview of its customer data. The registered customers should be stored in a MYSQL database, and it should be possible to edit the data and view an overview of the entries. Use PDO for database connection.  

**Requirements:**  
The tables should be structured as follows:  
- users: user_id, name, email, password  
- customers: company_id, company_name, contact_person, phone, address, created_by (which user created the entry), created_at (creation date), edited_at (modification date)  
- Relation: users 1 – n customers  

**Features:**  
- User Registration  
- User login  
- Creation of new customers via a contact form  
- Overview of all customers  
- Ability to edit and delete each entry  
- Logged-in users can see all entries in the system  
- However, logged-in users can only edit or delete their created entries (Hint: This can be solved using a session).  

**User Interface:**  
- Please use one of the CSS frameworks from the CSS Frameworks module for the user interface (GUI).  
- Design the customer management system to be user-friendly, with good user feedback on contact forms and clear indications if something goes wrong.  
- Pay attention to readability, avoid distracting colors, etc., while styling.  
- Also, consider responsive design for the tool and adjust your CSS accordingly. 
