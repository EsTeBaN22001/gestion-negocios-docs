# 27 — Estructura de repositorios

## Workspace común

La carpeta de trabajo puede contener:

```text
gestion-negocios/
├── AGENTS.md
├── README.md
├── .env.example
├── .gitignore
├── docker-compose.yml
├── docs/
├── agents/
├── backend/      ← repositorio Git independiente
└── frontend/     ← repositorio Git independiente
```

La documentación y los archivos del workspace común no sustituyen a los README de cada repositorio.

## Backend repository

Debe contener solamente lo necesario para construir y ejecutar el backend.

Debe incluir su propio:

- `.gitignore`;
- `README.md`;
- solución/proyecto .NET;
- configuración de Docker del backend si corresponde;
- tests cuando se incorporen.

## Frontend repository

Debe contener solamente lo necesario para construir y ejecutar Angular.

Debe incluir su propio:

- `.gitignore`;
- `README.md`;
- `package.json`;
- configuración Angular;
- configuración Docker del frontend si corresponde.

## Regla de sincronización

Si una decisión afecta a ambos repositorios, documentarla en el workspace común y reflejar en ambos README lo necesario para ejecutar cada parte.
