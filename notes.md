# Notas de configuración

Entorno: VPS Ubuntu 22.04 (1 GB RAM), OpenClaw v2026.7.1-2 como servicio systemd, acceso por SSH con clave pública.
- **Telegram con `dmPolicy: "pairing"` y `requireMention` en grupos.** OpenClaw no es multi-tenant y el agente tiene acceso al servidor, así que solo los usuarios que apruebo manualmente pueden usarlo.
- **Cuenta de Google separada de la personal** para Docs y Calendar, ya que el agente recibe permisos de escritura y actúa de forma autónoma.
- **API key de Composio acotada:** lectura general más escritura en Tool execution, Sessions y Connected accounts; se descartó *Proxy execute* por ser más amplio de lo necesario.
- **Error de sintaxis al añadir el bloque `channels`:** quedó una llave duplicada (`Extra data: line 137`). Desde entonces valido con `python3 -m json.tool` y guardo copia del último estado funcional antes de cada edición.
- **Instalación de la CLI de Composio:** faltaba `unzip` en el servidor y el binario quedó fuera del PATH (`~/.local/bin`). El agente diagnosticó y resolvió el primer problema por su cuenta.
- **Login sin navegador:** `composio login` espera abrir un navegador, inexistente en un servidor headless. Se resolvió con `composio login --user-api-key` usando el token generado desde el navegador local.
- **VS Code Remote descartado:** `vscode-server` consumía buena parte del gigabyte disponible y provocaba desconexiones SSH. Se trabajó directamente por terminal.

## Problemas encontrados
- `unzip` faltante al instalar Composio CLI — instalado manualmente.
- Login de Composio sin navegador → resuelto con `composio login --user-api-key`.
- Google Docs daba 403 (scopes insuficientes) hasta reconectar el OAuth con permisos de escritura.
- El MCP de Composio rechaza `x-api-key`; necesita `x-consumer-api-key` con una key del panel AI Clients.
