flowchart TD
    M[👑 Monster<br/>Manager] --> A[🧑‍💼 Adrien<br/>Sous-Chef]
    M --> S[💻 SEng]
    M --> AN[🧑‍🎓 Anthony<br/>Stagiaire]
    M --> SO[💡 Soline]
    M --> P[🔧 Philippe]

    A --> R[🧑‍🔬 Robin<br/>Externe]
    A --> D[🧑‍🔬 Damien<br/>Externe]

    classDef managerClass fill:#ffe082,stroke:#ffb300,stroke-width:2px
    classDef sousChefClass fill:#b2dfdb,stroke:#009688,stroke-width:2px
    classDef membreClass fill:#d1c4e9,stroke:#7e57c2
    classDef externeClass fill:#ffccbc,stroke:#d84315
    classDef stagiaireClass fill:#b3e5fc,stroke:#0288d1

    class M managerClass
    class A sousChefClass
    class S,SO,P membreClass
    class R,D externeClass
    class AN stagiaireClassrobi
