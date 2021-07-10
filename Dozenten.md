# Einem Studierenden für Rancher Ressourcen bereitstellen

Alle Benutzer mit einem Unix-Account können sich ohne vorherige Aktivierung bei Rancher anmelden. Studierende verfügen zu Anfang über keine Berechtigungen. Erst mit am Zuweisen von einem Projekt können Studierende 

Um für einen Studierenden ein neues Projekt anzulegen, wählen Sie im Cluster Explorer das Cluster `k8lab` aus. Anschließend im Reiter auf `Projects/Namespaces` klicken. 

![login](res/Neues_Projekt.png)

Anschließen können mit einen Klick auf`Add Project`` ein eines Projekt anlegen. 



![login](res/Project.png)

1. Vergeben Sie einen Namen (Studentenkürzel)

2. Fügen Sie den Studenten mit der Gruppe `Studenten Projekt` hinzu.

3. Setzen Sie ein Limit für die Kubernetes Ressourcen
   
   | Empfohlen                         | CPU Lim. | CPU Res. | RAM Lim. | RAM Res. | Storage |
   | --------------------------------- | -------- | -------- | -------- | -------- | ------- |
   | Let's Encrypt Zertifikat erzeugen | 1100     | 1100     | 1100     | 1100     | -       |
   | Wordpress                         | 1100     | 1100     | 1100     | 1100     | 20      |



| **Kontingentbezeichnung**       | **Beschreibung**                                           |
| ------------------------------- | ---------------------------------------------------------- |
| CPU-Limit                       | Maximale Anzahl an CPU-Kernen (in milliCPU)                |
| CPU-Reservierung                | Maximal mögliche Reservierung von CPU-Kernen (in milliCPU) |
| Speicherlimit                   | Maximale Benutzung von RAM (in MiB)                        |
| Speicherreservierung            | Maximal mögliche Reservierung von RAM (in MiB)             |
| Festplattenspeicherreservierung | Größe vom persistenten Speicher (in GB)                    |
| Service Load Balancer           | Anzahl von Load Balancer                                   |
| Service Node Ports              | Anzahl von Node Ports                                      |
| Pods                            | Anzahl von Pods                                            |
| Services                        | Anzahl von Services                                        |
| Config Maps                     | Anzahl von ConfigMaps                                      |
| Persistent Volume Claims        | Anzahl von Speicher Claims                                 |
| Replication Controllers         | Anzahl von Replikationskontroller                          |
| Secrets                         | Anzahl von Secrets                                         |
