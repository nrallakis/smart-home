Smart home layers:
```mermaid
flowchart TB
    A[Πηγές δεδομένων] --> B[Ενσωμάτωση δεδομένων]
    B --> C[Επεξεργασία δεδομένων]
    C --> D[Ομοσπονδία δεδομένων]
    D --> E[Οπτικοποίηση δεδομένων]
```

```mermaid
---
config:
  look: classic
  theme: redux-color
---
sequenceDiagram
  participant Sensors as Αισθητήρες
  participant HomeAssistant as Home Assistant
  participant Kafka as Στρώμα ενσωμάτωσης
  Sensors ->> HomeAssistant: Αποστολή μετρήσεων
  HomeAssistant ->> Kafka: Αποστολή κατάστασης
```
```mermaid
---
config:
  look: classic
  theme: redux
---
sequenceDiagram
    participant Superset as Apache Superset
    participant Trino as Trino
    participant Kafka as Kafka Topics
    Superset->>Trino: SQL ερώτημα
    Trino->>Kafka: Polling στα δεδομένα των topics
    Kafka-->>Trino: Επιστροφή δεδομένων
    Trino-->>Superset: Επιστροφή
```
```mermaid
---
config:
  look: classic
  theme: redux
---
flowchart TB
    A1 --> B[Home Assistant Green]
    A2 --> B
    A3 --> B

    subgraph Πηγές δεδομένων
        A1[Αισθητήρες θερμοκρασίας]
        A2[Συσκευές IoT]
        A3[Συστήματα αυτοματισμού]
    end
```
```mermaid
---
config:
  look: classic
  theme: redux
---
flowchart LR
    A1 --Zigbee--> B[Home Assistant Green]
    A2 --WiFi--> B
    A3 --Wifi--> B
    A4 --Wifi--> B
    A5 --Wifi--> B
    A6 --RF--> B
    A7 --Zigbee--> B
    

    subgraph Πηγές δεδομένων
        A1[Αισθητήρας θερμοκρασίας & υγρασίας]
        A2[Αισθητήρας κατανάλωσης ρεύματος]
        A3[Έξυπνη πρίζα]
        A4[Σκούπα ρομποότ]
        A5[Αφυγραντήρας]
        A6[Αισθητήρες πόρτας]
        A7[Έξυπνοι διακόπτες]
    end
```

```mermaid
---
config:
  look: classic
  theme: redux
---
flowchart LR
    A[Στρώμα πηγών δεδομένων] -->Kafka

    subgraph Kafka[Kafka Cluster]
      subgraph Broker 3      
        subgraph Topic N
        end
        subgraph Topic 2
        end
        subgraph Topic 1
        end
      end
      subgraph Broker 2      
        subgraph Topic N
        end
        subgraph Topic 2
        end
        subgraph Topic 1
        end
      end
      subgraph Broker      
        subgraph Topic N
        end
        subgraph Topic 2
        end
        subgraph Topic 1
        end
      end
    end

    Kafka --> Processor[Στρώμα επεξεργασίας]
    Processor --> Kafka
```
