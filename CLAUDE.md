# Capacitaciones RRHH — Movistar Arena

## Qué es este proyecto
Central de control de capacitaciones de RRHH para Movistar Arena (Buenos Aires).
App web 100% client-side (un solo archivo HTML), sin backend, sin build, sin dependencias.

## Estructura
```
capacitaciones-arena/
├── index.html        ← toda la app (HTML + CSS + JS en un solo archivo)
└── CLAUDE.md         ← este archivo
```

## Cómo correrlo
Abrí `index.html` directo en el navegador. No necesita servidor.
Para desarrollo con live reload podés usar:
```bash
npx serve .
# o
python3 -m http.server 8080
```

## Stack
- HTML + CSS + JS vanilla (sin frameworks)
- Fuente: Plus Jakarta Sans (Google Fonts)
- Persistencia: localStorage del navegador (clave: `caps_v3`)
- IA: Groq API (llamada directa desde el browser, sin proxy)

## API de IA — Groq
- Endpoint: `https://api.groq.com/openai/v1/chat/completions`
- Modelo: `llama-3.3-70b-versatile`
- Auth: `Authorization: Bearer gsk_...`
- La key se guarda en localStorage con clave `api_key_arena`
- Groq es gratuito: https://console.groq.com

## Funcionalidades actuales
1. **CRUD de capacitaciones** — nombre, estado, fecha, vencimiento, proveedor, notas
2. **Participantes por capacitación** — cada uno con su propio vencimiento de certificado
3. **Estados** — Realizada / Programada / En curso
4. **Vencimientos** — badge automático (Vigente / Vence pronto / Vencida) + barra visual
5. **Alertas** — vista dedicada con todos los vencimientos críticos ordenados por urgencia
6. **IA — Gmail** — genera email de alerta listo para copiar y pegar
7. **IA — Calendar** — genera título + descripción del evento para Google Calendar
8. **IA — Todo junto** — email + evento en una sola respuesta
9. **Filtros y búsqueda** — por estado y por texto libre
10. **Export/Import JSON** — para backup o compartir datos entre computadoras
11. **Persistencia** — los datos se guardan automáticamente en el navegador

## Mejoras posibles (backlog)
- [ ] Vincular Gmail real vía OAuth (enviar mails sin copiar/pegar)
- [ ] Vincular Google Calendar real vía OAuth (crear eventos directo)
- [ ] Firebase backend para compartir datos entre usuarios del equipo
- [ ] Notificaciones automáticas por email X días antes del vencimiento
- [ ] Panel multi-usuario (cada empleado ve sus propias capacitaciones)
- [ ] Exportar a Excel (.xlsx)
- [ ] Subir a GitHub Pages para acceso desde cualquier lado

## Contexto del proyecto
- Desarrollado para el área de RRHH de Movistar Arena (Buenos Aires Arena)
- El equipo ya usa GitHub Pages para otros proyectos internos (ej: prode Mundial 2026)
- Stack preferido del equipo: HTML estático + Google Sheets/Firebase como backend
- Idioma: español rioplatense

## Notas para Claude Code
- Mantené todo en un solo archivo `index.html` a menos que se pida explícitamente separar
- El CSS usa variables custom pero no Tailwind ni ningún framework
- Los datos de ejemplo están hardcodeados en el array `caps` dentro del JS
- La función `render()` es el punto de entrada principal que redibuja toda la UI
- Para agregar una nueva vista: crear función `renderNombre()` y agregar case en `render()`
