```mermaid
flowchart TD
    A[Début] --> B[Question en langage naturel reçue]
    B --> C[Analyse NLP (Compréhension du langage)]
    C --> D[Génération de la requête SQL]
    D --> E[Validation de la requête SQL]
    E --> F[Exécution sur base Oracle]
    F --> G[Résultat brut de la base de données]
    G --> H[Formatage en réponse lisible]
    H --> I[Réponse claire pour l'utilisateur]
    I --> J[Fin]
```
