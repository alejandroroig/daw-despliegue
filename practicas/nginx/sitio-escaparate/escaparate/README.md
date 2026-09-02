# Escaparate — distribución estática

Versión completamente estática del catálogo Escaparate.

No utiliza:

- Java
- Spring Boot
- PostgreSQL
- API

Los productos se cargan desde:

```text
data/productos.json
```

## Contenido

```text
escaparate/
├── index.html
├── config.js
├── css/
├── js/
└── data/
    └── productos.json
```

## Probar localmente

No abras `index.html` directamente con `file://`, porque el navegador puede bloquear la carga del JSON.

Desde la carpeta que contiene el proyecto:

```powershell
py -m http.server 8001 --directory escaparate
```

Abre:

```text
http://localhost:8001
```

Esta distribución puede publicarse en cualquier servidor de contenido estático.

## Nota

Trabaja únicamente con los ficheros y requisitos indicados en la actividad. No necesitas conocer otras variantes de Escaparate.
