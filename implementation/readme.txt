instruction to run the website : 


Anleitung 
5.1 Einrichtung der Datenbank

Xampp starten. Dort auch MySQL starten und über Admin auf phpmyAdmin gehen. Eine Datenbank mit den Namen name_db erstellen und name_db.sql file importieren oder unter SQL innerhalb der Datenbank die folgenden Anweisungen eingeben, um die entsprechenden 4 Tabellen erstellen zu lassen. 

phpMyAdmin SQL Dump
version 5.2.1
https://www.phpmyadmin.net/
--
Host: 127.0.0.1
Generation Time: Nov 16, 2024 at 12:41 AM
Server version: 11.5.2-MariaDB
PHP Version: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
Database: `name_db`
--

--------------------------------------------------------

--
Table structure for table `comments`
--

CREATE TABLE `comments` (
`text` varchar(5000) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL,
`user` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL,
`time` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL,
`taskname` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_swedish_ci;

--
Dumping data for table `comments`
--

INSERT INTO `comments` (`text`, `user`, `time`, `taskname`) VALUES
('this task is overdue ;((', 'developer', '2024-11-16 00:38:18', 'Example overdue task'),
('Good job Team!', 'developer', '2024-11-16 00:39:43', 'Example normal task');

--------------------------------------------------------

--
Table structure for table `projects`
--

CREATE TABLE `projects` (
`projectName` varchar(255) NOT NULL,
`projectDetails` text NOT NULL,
`projectProgress` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_swedish_ci;

--
Dumping data for table `projects`
--

INSERT INTO `projects` (`projectName`, `projectDetails`, `projectProgress`) VALUES
('Example Project', 'this is an example project !\nWelcome to our website :)', 0);

--------------------------------------------------------

--
Table structure for table `tasks`
--

CREATE TABLE `tasks` (
`taskname` varchar(255) NOT NULL,
`prio` int(11) NOT NULL,
`owner` varchar(255) DEFAULT NULL,
`assigned` varchar(255) DEFAULT NULL,
`description` text DEFAULT NULL,
`status` int(11) DEFAULT NULL,
`projectName` varchar(255) DEFAULT NULL,
`deadline` datetime DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_swedish_ci;

--
Dumping data for table `tasks`
--

INSERT INTO `tasks` (`taskname`, `prio`, `owner`, `assigned`, `description`, `status`, `projectName`, `deadline`) VALUES
('Example normal task', 1, 'developer', 'developer', 'This is an example of a normal task that is currently being worked on and the deadline is still open :)', 4, 'Example Project', '2028-01-01 00:00:00'),
('Example overdue task', 2, 'developer', 'developer', 'deadline expired! thats why it\'s red!', 3, 'Example Project', '2020-01-01 00:00:00');

--------------------------------------------------------

--
Table structure for table `users`
--

CREATE TABLE `users` (
`id` int(11) NOT NULL,
`username` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL,
`password` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL,
`rank` int(1) NOT NULL,
`email` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_swedish_ci;

--
Indexes for dumped tables
--

--
Indexes for table `users`
--
ALTER TABLE `users`
ADD PRIMARY KEY (`id`);

--
AUTO_INCREMENT for dumped tables
--

--
AUTO_INCREMENT for table `users`
--
ALTER TABLE `users`
MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=14;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;



5.2 Konfiguration
Das Projekt in VSCode laden. In der File config.json die passenden Daten zur Datenbankverbindung eintragen, wie das Password oder der gewünschte Port, sowie die E-Mail-Adresse und das Passwort der E-Mail, die die E-Mails versendet: 
{
    "db": {
      "host": "localhost",
      "user": "root",
      "password": "",
      "database": "name_db"
    },
    "sessionSecret": "geheimnisvollerSchlüssel",
    "sessionMaxAge": 600000,
    "port": 3001,
    "email": {
    "user": "__________________",
    "pass": "***********",
    "subject": {
      "deadlineNear": "Aufgabe steht kurz vor Ablauf",
      "deadlineMissed": "Deadline überschritten"
    },
    "intervalInMinutes": 1
    }
  }

5.3 Start der Webseite   
Um die Website zum Laufen zu bringen muss man zum einen die Datenbank wie in 5.1 beschrieben einrichten und bei Xampp den Apache Webserver und MySQL angeschaltet haben. Im Terminal in VSCode node server.js eingeben. Eventuell gibt es in den terminalen Fehlermeldungen, dass gewisse Module nicht vorhanden sind. Diese mit npm install noch installieren. Und dann den Server über die Ausgabe im Terminal öffnen. So kommt man auf die Seite zum Anmelden/Registrieren. Sollte ein Fehler auftreten, sollte dieser in Terminal dokumentiert werden. 



5.4 Anmeldung
Wenn man sich auf der Website zu Beginn anmeldet, bekommt der erste User die Rolle des Admins. Die weiteren User werden zu normalen Mitarbeitern. Ist die Registrierung erfolgreich erscheint unter den Eingabefelder eine Benachrichtigung, wenn man sie nicht sieht, dann ist die Bildschirm-zoom zu groß. Nach dem man sich registriert hat, kann man sich anmelden und kommt auf eine Seite, auf der alle bestehenden Projekte angezeigt werden, in denen man mitarbeitet. Sollte man den Rang des Admins ändern (es gibt keinen Admin mehr), dann gibt es auf der Website keine Möglichkeit mehr dies zu ändern. Das muss man dann direkt in der Datenbank machen. Stelle deshalb sicher, dass es immer mindesten einen Admin gibt.

5.4 Bedienen der Software
Auf dem Projektdashboard kann man nach dem Erstellen eines Projektes dieses noch bearbeiten. Ebenfalls können hier die verschiedenen Benutzerberechtigungen verwalten werden. Über den Details-Button gelangt man auf das Taskboard, auf dem man neue Task erstellen und alte bearbeiten kann. Task die hierbei Farblich hervorgehoben sind, haben ihre Deadline überschritten. 

5.6 Die verschiedenen Rollen

Es gibt verschiedene Rollen wie Admin und Manager und User, die manche Funktionen nicht verwenden können. So kann der Admin beispielsweise die Mitarbeiter bearbeiten und deren Rank ändern. Für jede Rollen gibt es im Code ein eigenes Dashboard.
•	Der Admin darf alles
•	Der Manager der darf keine Benutzer bearbeiten 
•	Der User kann keine Projekte erstellen und bearbeiten, keine Benutzer bearbeiten und kann ownership und assigned bei Tasks nicht ändern

