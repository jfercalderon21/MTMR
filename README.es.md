# MTMR — Mejoras para Apple Silicon (fork comunitario)

[English](README.md) · [Proyecto original](https://github.com/Toxblh/MTMR) · [Cierre automático de grupos](docs/automatic-group-closing.md) · [Compilación Apple Silicon](docs/apple-silicon-build.md)

> **Estado: documentación preliminar.** Este repositorio es un fork público de MTMR. Todavía no se ha incorporado el código fuente modificado que se conserva localmente en la Mac. Actualmente el código procede del proyecto original; las mejoras descritas no deben considerarse disponibles ni verificadas en este fork.

## Objetivo

Documentar y compartir modificaciones locales de **My TouchBar My Rules (MTMR)** para usuarios de MacBook Pro con Touch Bar, manteniendo los créditos, el historial y la licencia del proyecto original.

## Cambios previstos

| Área | Situación |
| --- | --- |
| Cierre automático de un grupo tras activar una acción | Documentado; falta incorporar y comprobar el código |
| Compilación nativa ARM64 y universal (ARM64 + x86_64) | Guía preliminar; falta reproducir la compilación desde el fork |
| Firma ad hoc y permisos de Accesibilidad | Notas técnicas; falta validar la instalación |
| Pulsación corta ⌘Q y larga ⌘W | Personalización local; ejemplo pendiente |
| Consumo de CPU | Mediciones diagnósticas; no se afirma una optimización |

## Documentación técnica

- [Cierre automático de grupos (inglés)](docs/automatic-group-closing.md)
- [Guía de compilación y verificación Apple Silicon (inglés)](docs/apple-silicon-build.md)

## Próximos pasos

1. Identificar el estado exacto del código fuente local y compararlo con el repositorio original.
2. Incorporar las modificaciones verificadas mediante commits separados.
3. Compilar y comprobar el funcionamiento en macOS con Apple Silicon.
4. Publicar instrucciones definitivas y, solo después de las pruebas, considerar una versión descargable.

## Instalación y advertencia

**Todavía no hay una versión binaria validada de este fork.** Las instrucciones de instalación y los enlaces a versiones que aparecen en el [README principal](README.md) pertenecen al proyecto original. No deben confundirse con una versión personalizada publicada por este fork.

## Créditos y licencia

Proyecto original: [Toxblh/MTMR](https://github.com/Toxblh/MTMR), desarrollado por sus colaboradores originales. Este fork conserva la licencia [MIT](LICENSE) y las atribuciones originales. La documentación complementaria no implica respaldo oficial de los mantenedores.
