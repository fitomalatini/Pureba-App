# Pureba-App: escritorio remoto (fork de RustDesk)

Este repositorio parte del código abierto de [RustDesk](https://github.com/rustdesk/rustdesk)
(licencia **AGPL-3.0**, ver `LICENCE`). Si distribuyes el programa modificado, la licencia te
obliga a publicar también su código fuente con los cambios.

## Primer objetivo: Windows

### 1. Compilar el cliente
1. En GitHub ve a **Actions → "Compilar cliente Windows" → Run workflow** (rama `main`).
2. Tarda unos 40–60 min la primera vez (las siguientes, menos, gracias a la caché).
3. Descarga el artefacto `cliente-windows-x64` y ejecuta `rustdesk.exe`.

### 2. (Recomendado) Usar tu propio servidor
Sin servidor propio el cliente usa los servidores públicos de RustDesk.
1. En un VPS Linux con Docker: `cd servidor && docker compose up -d`.
2. Copia el contenido de `servidor/data/id_ed25519.pub`.
3. En GitHub: **Settings → Secrets and variables → Actions → Variables** y crea:
   - `RENDEZVOUS_SERVER` = IP o dominio del VPS
   - `RS_PUB_KEY` = la clave del paso 2
4. Vuelve a lanzar la compilación.

## Dónde tocar el código
| Qué | Dónde |
|---|---|
| Servidor y clave por defecto | `libs/hbb_common/src/config.rs` (`RENDEZVOUS_SERVERS`, `RS_PUB_KEY`) |
| Nombre de la app | `APP_NAME` en `libs/hbb_common/src/config.rs`, `Cargo.toml`, `flutter/windows/runner/` |
| Interfaz (Flutter) | `flutter/lib/` |
| Lógica Rust (captura, entrada, red) | `src/` |
| Iconos | `res/` |

## Próximos pasos
- Cambiar nombre e iconos (marca propia: no se puede usar la marca "RustDesk").
- Cliente iOS: el proyecto Flutter ya incluye `flutter/ios`, pero hay que compilarlo en un Mac con Xcode.
