# Struttura del Database per il Gestionale Officina

## Tabelle

---

### 1. **Customers** (`customers`)
| Field            | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico del cliente       |
| first_name       | VARCHAR(100) | Nome del cliente                      |
| last_name        | VARCHAR(100) | Cognome del cliente                   |
| email            | VARCHAR(150) | Email del cliente                     |
| phone            | VARCHAR(50)  | Numero di telefono                    |
| address          | TEXT         | Indirizzo completo                    |
| tax_code         | VARCHAR(16)  | Codice fiscale                        |
| vat_number       | VARCHAR(20)  | Partita IVA                           |
| company_name     | VARCHAR(150) | Ragione sociale (se azienda)          |
| pec              | VARCHAR(150) | Posta Elettronica Certificata (PEC)   |
| unique_code      | VARCHAR(50)  | Codice univoco per fatturazione       |
| creation_date    | DATETIME     | Data di registrazione del cliente      |

---

### 2. **Cars** (`cars`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico dell'auto         |
| customer_id      | INT (FK)     | ID del cliente proprietario dell'auto  |
| brand            | VARCHAR(100) | Marca dell'auto                       |
| model            | VARCHAR(100) | Modello dell'auto                     |
| license_plate    | VARCHAR(20)  | Targa dell'auto                       |
| chassis_number   | VARCHAR(50)  | Numero di telaio                      |
| year             | YEAR         | Anno di immatricolazione              |
| notes            | TEXT         | Note aggiuntive sull'auto             |

---

### 3. **Work Orders** (`work_orders`)
| Field           | Type          | Description                                                  |
|-----------------|---------------|--------------------------------------------------------------|
| id              | INT (PK)      | Identificativo unico della scheda                            |
| customer_id     | INT (FK)      | ID del cliente associato                                     |
| car_id          | INT (FK)      | ID dell'auto associata                                       |
| workshop_id     | INT (FK)      | ID dell'officina associata                                   |
| car_mileage     | INT           | Chilometraggio dell'auto al momento dell'ingresso            |
| entry_date      | DATETIME      | Data ingresso auto                                           |
| delivery_date   | DATETIME      | Data consegna auto                                           |
| closure_date    | DATETIME      | Data di chiusura della scheda                                |
| to_be_invoiced  | BOOLEAN       | Indica se la scheda è da fatturare                           |
| creation_date   | DATETIME      | Data di creazione della scheda                               |
| status          | ENUM          | Stato della scheda (e.g., "Aperta", "Chiusa")                |
| notes           | TEXT          | Note generali sulla scheda                                   |

---

### 4. **Workshops** (`workshops`)
| Field           | Type         | Description                           |
|------------------|--------------|--------------------------------------|
| id               | INT (PK)     | Identificativo unico dell'officina    |
| name             | VARCHAR(150) | Nome dell'officina                    |
| address          | TEXT         | Indirizzo completo                    |
| phone            | VARCHAR(50)  | Numero di telefono                    |
| email            | VARCHAR(150) | Email dell'officina                   |
| vat_number       | VARCHAR(20)  | Partita IVA                           |
| logo             | VARCHAR(20)  | Url logo                              |
| creation_date    | DATETIME     | Data di registrazione dell'officina   |

---

### 5. **Users** (`users`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico dell'utente       |
| first_name       | VARCHAR(100) | Nome dell'utente                      |
| last_name        | VARCHAR(100) | Cognome dell'utente                   |
| email            | VARCHAR(150) | Email dell'utente                     |
| password_hash    | TEXT         | Hash della password                   |
| role             | ENUM         | Ruolo dell'utente (e.g., "Amministratore", "Tecnico") |
| creation_date    | DATETIME     | Data di registrazione                 |

---

### 6. **User-Workshop Relationship** (`user_workshops`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico della relazione  |
| user_id          | INT (FK)     | ID dell'utente                        |
| workshop_id      | INT (FK)     | ID dell'officina                      |
| role             | ENUM         | Ruolo specifico nell'officina (e.g., "Manager", "Operatore") |
| creation_date    | DATETIME     | Data di associazione                   |

---

### 7. **Work Items** (`work_items`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico della voce        |
| work_order_id    | INT (FK)     | ID della scheda di lavoro              |
| description      | TEXT         | Descrizione della lavorazione          |
| cost             | DECIMAL(10,2)| Costo della lavorazione                |
| quantity         | INT          | Quantità (se applicabile)              |
| total            | DECIMAL(10,2)| Totale (costo x quantità)              |

---

### 8. **System Logs** (`system_logs`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico del log           |
| timestamp        | DATETIME     | Data e ora dell'evento                |
| level            | ENUM         | Livello del log (e.g., "INFO", "WARN", "ERROR") |
| message          | TEXT         | Messaggio del log                     |
| user_id          | INT (FK)     | ID dell'utente (se applicabile)        |

---

### 9. **User Actions** (`user_actions`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico dell'azione       |
| user_id          | INT (FK)     | ID dell'utente che ha effettuato l'azione |
| timestamp        | DATETIME     | Data e ora dell'azione                |
| action           | ENUM         | Tipo di azione (e.g., "Accesso", "Creazione Scheda", "Modifica Scheda", "Cancellazione Scheda") |
| entity           | VARCHAR(50)  | Nome dell'entità coinvolta (e.g., "work_orders") |
| entity_id        | INT          | ID dell'entità coinvolta              |

---

### 10. **Notifications** (`notifications`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico della notifica    |
| workshop_id      | INT (FK)     | ID dell'officina destinataria          |
| message          | TEXT         | Contenuto della notifica               |
| status           | ENUM         | Stato della notifica (e.g., "Nuova", "Letta") |
| creation_date    | DATETIME     | Data di creazione                     |

---

### 11. **Car Damages** (`car_damages`)
| Field           | Type         | Description                            |
|------------------|--------------|---------------------------------------|
| id               | INT (PK)     | Identificativo unico del danno         |
| work_order_id    | INT (FK)     | ID della scheda di lavoro              |
| position         | VARCHAR(100) | Posizione del danno (e.g., "Portiera destra") |
| description      | TEXT         | Descrizione del danno                  |
| attached_photo   | TEXT         | Percorso del file allegato (foto danno) |

---

### 12. **Attachments** (`attachments`)
| Field           | Type         | Description                            |
|------------------|--------------|----------------------------------------|
| id               | INT (PK)     | Identificativo unico del file          |
| work_order_id    | INT (FK)     | ID della scheda di lavoro              |
| file_name        | VARCHAR(255) | Nome del file                          |
| file_path        | TEXT         | Percorso del file nel sistema          |
| upload_date      | DATETIME     | Data di caricamento                    |

---

## Relazioni Chiave
1. **Workshops → Users**: Ogni officina può avere più utenti.
2. **Customers → Cars**: Ogni cliente può avere più auto.
3. **Customers → Work Orders**: Ogni cliente può avere più schede di lavoro.
4. **Cars → Work Orders**: Ogni auto può essere associata a più schede di lavoro.
5. **Work Orders → Work Items**: Ogni scheda può contenere più voci di lavorazione.
6. **Work Orders → Car Damages**: Ogni scheda può documentare più danni all'auto.
7. **Work Orders → Attachments**: Ogni scheda può avere più file allegati.
8. **Users → User Actions**: Ogni utente può generare molte azioni.
9. **Users → Workshops (tramite `user_workshops`)**: Ogni utente può essere associato a più officine, con un ruolo specifico per ogni officina.
10. **Workshops → Notifications**: Ogni officina può ricevere molte notifiche.

---

## Ottimizzazioni Future
- **Indici**: Creare indici su `customer_id`, `car_id`, `work_order_id`, `user_id` per migliorare le prestazioni delle query.
- **Log di Audit**: Implementare un sistema per tracciare dettagliatamente le modifiche effettuate dagli utenti.
- **Automazioni**: Aggiungere trigger per notifiche automatiche basate su eventi (e.g., scadenze, avanzamento lavori).