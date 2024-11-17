# Elenco degli Endpoint per il Gestionale Officina

## **Autenticazione e Autorizzazione**
| Metodo | Endpoint         | Descrizione                                             | Parametri                                  | Risposta                              |
|--------|------------------|---------------------------------------------------------|-------------------------------------------|---------------------------------------|
| POST   | `/auth/login`    | Effettua l'accesso di un utente                         | email, password                           | Token JWT, ruolo utente, officine     |
| POST   | `/auth/logout`   | Effettua il logout dell'utente                          | N/A                                       | N/A                                   |
| GET    | `/auth/me`       | Recupera le informazioni dell'utente autenticato        | N/A                                       | Dati utente, officine, ruolo          |

---

## **Officine**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/workshops`         | Recupera l'elenco delle officine associate            | Nome officina, città                      | Lista officine                        |
| POST   | `/workshops`         | Crea una nuova officina                               | Nome, indirizzo, partita IVA, email, tel. | Officina creata                       |
| PUT    | `/workshops/{id}`    | Modifica i dati di un'officina esistente              | Nome, indirizzo, partita IVA, email, tel. | Officina aggiornata                   |
| DELETE | `/workshops/{id}`    | Elimina un'officina                                   | N/A                                       | N/A                                   |

---

## **Clienti**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/customers`         | Recupera l'elenco dei clienti                        | Nome, cognome, codice fiscale, targa      | Lista clienti                        |
| POST   | `/customers`         | Crea un nuovo cliente                                | Nome, cognome, PEC, codice univoco, email, tel., indirizzo | Cliente creato   |
| PUT    | `/customers/{id}`    | Modifica i dati di un cliente                        | Dati aggiornati del cliente               | Cliente aggiornato                    |
| DELETE | `/customers/{id}`    | Elimina un cliente                                   | N/A                                       | N/A                                   |

---

## **Auto**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/cars`              | Recupera l'elenco delle auto associate               | Targa, marca, modello, cliente ID         | Lista auto                            |
| POST   | `/cars`              | Aggiunge una nuova auto                              | Cliente ID, marca, modello, targa, telaio | Auto creata                           |
| PUT    | `/cars/{id}`         | Modifica i dati di un'auto                           | Dati aggiornati dell'auto                 | Auto aggiornata                       |
| DELETE | `/cars/{id}`         | Elimina un'auto                                      | N/A                                       | N/A                                   |

---

## **Schede di Lavoro**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/work-orders`       | Recupera l'elenco delle schede di lavoro             | Stato, cliente, auto, intervallo date     | Lista schede                          |
| GET    | `/work-orders/{id}`  | Recupera i dettagli di una specifica scheda          | N/A                                       | Dettagli scheda                       |
| POST   | `/work-orders`       | Crea una nuova scheda                                | Cliente ID, auto ID, officina ID, km, note, stato | Scheda creata            |
| PUT    | `/work-orders/{id}`  | Modifica una scheda di lavoro esistente              | Dati aggiornati della scheda              | Scheda aggiornata                     |
| DELETE | `/work-orders/{id}`  | Elimina una scheda di lavoro                         | N/A                                       | N/A                                   |

---

## **Voci di Lavorazione**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/work-items`        | Recupera le voci di lavorazione per una scheda        | Scheda ID, descrizione                    | Lista voci                            |
| POST   | `/work-items`        | Aggiunge una nuova voce di lavorazione               | Scheda ID, descrizione, costo, quantità   | Voce creata                           |
| PUT    | `/work-items/{id}`   | Modifica una voce di lavorazione                     | Dati aggiornati della voce                | Voce aggiornata                       |
| DELETE | `/work-items/{id}`   | Elimina una voce di lavorazione                      | N/A                                       | N/A                                   |

---

## **Danni Auto**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/car-damages`       | Recupera l'elenco dei danni per una scheda            | Scheda ID                                 | Lista danni                           |
| POST   | `/car-damages`       | Aggiunge un danno a una scheda                        | Scheda ID, posizione, descrizione, foto   | Danno creato                          |
| DELETE | `/car-damages/{id}`  | Elimina un danno documentato                         | N/A                                       | N/A                                   |

---

## **File Allegati**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/attachments`       | Recupera l'elenco dei file allegati per una scheda    | Scheda ID                                 | Lista file                            |
| POST   | `/attachments`       | Carica un file allegato                              | Scheda ID, file                           | File caricato                         |
| DELETE | `/attachments/{id}`  | Elimina un file allegato                             | N/A                                       | N/A                                   |

---

## **Notifiche**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/notifications`     | Recupera le notifiche per l'utente e le sue officine  | Stato (opzionale)                         | Lista notifiche                       |
| PUT    | `/notifications/{id}`| Segna una notifica come letta                        | N/A                                       | Notifica aggiornata                   |

---

## **Log di Sistema**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/system-logs`       | Recupera i log di sistema                             | Intervallo date, livello log, utente      | Lista log                             |

---

## **Azioni Utente**
| Metodo | Endpoint             | Descrizione                                           | Parametri                                  | Risposta                              |
|--------|----------------------|-------------------------------------------------------|-------------------------------------------|---------------------------------------|
| GET    | `/user-actions`      | Recupera le azioni effettuate dagli utenti            | Utente, tipo azione, intervallo date      | Lista azioni                          |
