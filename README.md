## Docker Compose-File

Dieses README erklärt die verschiedenen Elemente des Docker Compose-Files in meinem Beispielprojekt, das einen Nginx-Frontend, einen PHP-FPM-Backend und eine MySQL-Datenbank verwendet.

Das Docker Compose-File definiert drei Services: `frontend`, `backend` und `db`.

- `frontend`: Nginx-Service, der als Webserver für statische HTML-Dateien fungiert und PHP-Anfragen an den Backend-Service weiterleitet.
- `backend`: PHP-FPM-Service, der PHP-Dateien ausführt und auf Port 9000 läuft.
- `db`: MySQL-Service, der die Datenbank für das Backend bereitstellt.

## Docker Compose-File Erklärung

### version

Gibt die verwendete Version der Docker Compose-Syntax an. In diesem Beispiel wird Version 3.9 verwendet.

### services

Definiert die verschiedenen Services, die in der Anwendung verwendet werden. In diesem Beispiel gibt es drei Services: `frontend`, `backend` und `db`.

#### frontend

- `image`: Gibt das Docker-Image für den Frontend-Service an. Hier verwenden wir das offizielle Nginx-Image.
- `build`: Gibt den Pfad zum Dockerfile für den Frontend-Build-Prozess an. In diesem Fall verwenden wir den Ordner `./frontend`.
- `ports`: Listet die Port-Bindungen für den Container auf. Hier verbinden wir den Port 80 des Hosts mit dem Port 80 des Containers.
- `depends_on`: Gibt die Abhängigkeiten dieses Services an. In diesem Beispiel hängt der Frontend-Service vom Backend-Service ab.
- `volumes`: Bindet Dateien und Ordner vom Host-System in den Container ein. Hier binden wir die `nginx.conf`-Datei und das `html`-Verzeichnis auf dem Host-System in die entsprechenden Verzeichnisse im Nginx-Container.

#### backend

- `image`: Gibt das Docker-Image für den Backend-Service an. Hier verwenden wir das offizielle PHP-FPM-Image.
- `build`: Gibt den Pfad zum Dockerfile für den Backend-Build-Prozess an. In diesem Fall verwenden wir den Ordner `./backend`.
- `ports`: Listet die Port-Bindungen für den Container auf. Hier verbinden wir den Port 9000 des Hosts mit dem Port 9000 des Containers.
- `depends_on`: Gibt die Abhängigkeiten dieses Services an. In diesem Beispiel hängt der Backend-Service vom DB-Service ab.
- `environment`: Setzt Umgebungsvariablen im Container. In diesem Fall setzen wir die Umgebungsvariablen für den MySQL-Host, -Benutzer, -Passwort und -Datenbank.
- `volumes`: Bindet Dateien und Ordner vom Host-System in den Container ein. Hier binden wir das `./backend`-Verzeichnis auf dem Host-System in das `/var/www/html`-Verzeichnis im Container.

#### db

- `image`: Gibt das Docker-Image für den DB-Service an. Hier verwenden wir das offizielle MySQL-Image.
- `environment`: Setzt Umgebungsvariablen im Container. In diesem Fall setzen wir die Umgebungsvariablen für das MySQL-Root-Passwort, den MySQL-Benutzer, das MySQL-Passwort und die MySQL-Datenbank.
- `volumes`: Bindet Dateien und Ordner vom Host-System in den Container ein. Hier binden wir das `./mysql-data`-Verzeichnis auf dem Host-System in das `/var/lib/mysql`-Verzeichnis im Container ein.

