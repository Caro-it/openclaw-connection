# OpenClaw — Conexión con Telegram, Google Docs y Google Calendar

Entrega del proyecto *Conecta tu Agente: Telegram, Google Docs y Calendario* del bootcamp de AI Engineering de 4Geeks Academy.

## Qué contiene

Un asistente de IA autoalojado (OpenClaw) corriendo en un VPS, accesible desde Telegram y capaz de crear documentos en Google Docs y eventos en Google Calendar a través del MCP de Composio.

## Arquitectura

```
Telegram  ──►  OpenClaw Gateway (VPS)  ──►  LiteLLM  ──►  modelo
                        │
                        └──►  MCP de Composio  ──►  Google Docs / Calendar
```

- **Servidor:** VPS Ubuntu 22.04 (1 GB RAM, 1 vCPU), acceso por SSH con clave pública
- **Gateway:** OpenClaw v2026.7.1-2 como servicio systemd de usuario, puerto 18789
- **Modelo:** vía endpoint LiteLLM
- **Canal:** Telegram con política de emparejamiento manual
- **Integraciones:** Composio MCP (`https://connect.composio.dev/mcp`)

## Evidencias

| Archivo | Contenido |
|---|---|
| `01-telegram-conectado.png` | El agente responde en Telegram con su identidad personalizada |
| `02-composio-mcp.png` | Toolkits de Composio activos y visibles para el agente |
| `03-documento-google-docs.png` | Documento creado en Google Docs |
| `04-evento-calendario.png` | Evento creado en Google Calendar |
| `05-conversacion-telegram.pdf` | Conversación completa: solicitud, preguntas del agente y confirmación |
| `notes.md` | Decisiones de configuración y problemas encontrados |

## Notas de seguridad

Ninguna credencial se incluye en este repositorio. El archivo `openclaw.json`, que contiene el token del bot y las claves de API, permanece únicamente en el servidor y fuera del workspace versionado. Las integraciones de Google están conectadas a una cuenta de prueba, separada de cualquier cuenta personal.

---


