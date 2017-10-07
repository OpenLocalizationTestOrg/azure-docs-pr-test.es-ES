---
title: "referencia de configuración móvil aaaWindows 10 | Documentos de Microsoft"
description: Una lista completa de todas las configuraciones de Hola que movido o una copia de seguridad de Windows 10.
services: active-directory
keywords: enterprise state roaming, nube de windows
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 17cffc3e-2928-4235-91f7-a685bd6bdcbf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 381e2220b698bb0e477c207984ff96c03ed132ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-roaming-settings-reference"></a>Referencia de la configuración de movilidad de Windows 10
Hola aquí te mostramos una lista completa de todas las configuraciones de Hola que movido o una copia de seguridad de Windows 10. 

## <a name="devices-and-endpoints"></a>Interfaces y puntos de conexión
Vea Hola para obtener un resumen de los dispositivos de Hola y tipos de cuenta que son compatibles con la sincronización de hello, copia de seguridad, en la tabla siguiente y restaurar el marco de trabajo en Windows 10.

| Tipo de cuenta y operación | Escritorio | Móvil |
| --- | --- | --- |
| Azure Active Directory: sincronización |Sí |No |
| Azure Active Directory: copia de seguridad/restauración |No |No |
| Cuenta de Microsoft: sincronización |Sí |Sí |
| Cuenta de Microsoft: copia de seguridad/restauración |No |Sí |

## <a name="what-is-backup"></a>¿Qué es una copia de seguridad?
Configuración de Windows de sincronización normalmente de forma predeterminada, pero algunas configuraciones solo se copian de seguridad, como lista de Hola de las aplicaciones instaladas en un dispositivo. La característica Backup está destinada solo para dispositivos móviles y no está disponible actualmente para los usuarios de Enterprise State Roaming. Copia de seguridad usa una cuenta de Microsoft y almacena los datos de aplicación y la configuración de hello en OneDrive. Si un usuario deshabilita la sincronización en dispositivo hello mediante la aplicación de configuración de hello, datos de la aplicación que normalmente se sincroniza se convierte en copia de seguridad solo. Datos de copia de seguridad solo pueden obtenerse a través de la operación de restauración de Hola durante la primera ejecución de un nuevo dispositivo de Hola. Las copias de seguridad se puede deshabilitar mediante la configuración de dispositivos de hello y se pueden administrar y eliminar a través de la cuenta de OneDrive del usuario de Hola.

## <a name="windows-settings-overview"></a>Introducción a la configuración de Windows
Hello grupos de configuración siguientes están disponibles para la sincronización de configuración de los usuarios finales tooenable o deshabilitar en dispositivos Windows 10.

* Tema: fondo de escritorio, icono de usuario, posición de la barra de tareas, etc. 
* Configuración de Internet Explorer: historial de exploración, direcciones URL escritas, favoritos, etc. 
* Contraseñas: [Caja de seguridad de credenciales de Windows](https://technet.microsoft.com/library/jj554668.aspx), incluidos perfiles de Wi-Fi 
* Preferencias de idioma: diccionario de ortografía, configuración de idioma del sistema 
* Facilidad de acceso: narrador, teclado en pantalla, lupa 
* Otras configuraciones de Windows: consultar Detalles de configuración de Windows

![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-individual-sync-settings.png)

Es posible habilitar o deshabilitar la sincronización de un grupo de configuración del explorador Edge a través de la opción de menú Configuración del explorador Edge.

![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-sync-content.png)

## <a name="windows-settings-details"></a>Detalles de configuración de Windows
En hello en la tabla siguiente, las demás entradas en la columna de grupo de configuración de hello hace referencia toosettings que puede deshabilitarse yendo tooSettings > cuentas > sincronizar la configuración > configuración de otras ventanas. 

Entradas internas en la columna de grupo de configuración de Hola refieren toosettings y aplicaciones que solo se puede deshabilitar de la sincronización dentro de la propia aplicación Hola o al deshabilitar la sincronización de dispositivo completo Hola con administración de dispositivos móviles (MDM) o la configuración de directiva de grupo de.
Valores de configuración que no se transmiten o sincronización no pertenecerá tooa grupo.

| Settings | Escritorio | Móvil | Grupo |
| --- | --- | --- | --- |
| **Cuentas**: imagen de la cuenta |sync |X |Tema |
| **Cuentas**: otras configuraciones de la cuenta |X |X | |
| **Ancho de banda móvil avanzado**: conexión a Internet que comparte el nombre de red (permite la detección automática de zonas con cobertura inalámbrica móvil a través de Bluetooth) |X |X |Contraseñas |
| **Datos de la aplicación**: las aplicaciones individuales pueden sincronizar datos |sincronización copia de seguridad |sincronización copia de seguridad |interno |
| **Lista de aplicaciones**: lista de aplicaciones instaladas |X |backup |Otros |
| **Bluetooth**: toda la configuración de Bluetooth |X |X | |
| **Símbolo del sistema**: configuración predeterminada del símbolo del sistema. |sync |X | |
| **Credenciales**: Caja de seguridad de credenciales |sync |sync |contraseña |
| **Fecha, hora y región**: hora automática (sincronización de hora de Internet) |sync |sync |language |
| **Fecha, hora y región**: formato de 24 horas |sync |X |language |
| **Fecha, hora y región**: fecha y hora |sync |X |language |
| **Fecha, hora y región**: zona horaria | |X |language |
| **Fecha, hora y región**: horario de verano |sync |X |language |
| **Fecha, hora y región**: país o región |sync |X |language |
| **Fecha, hora y región**: primer día de la semana |sync |X |language |
| **Fecha, hora y región**: formato de región (configuración regional) |sync |X |language |
| **Fecha, hora y región**: fecha corta |sync |X |language |
| **Fecha, hora y región**: fecha larga |sync |X |language |
| **Fecha, hora y región**: hora corta |sync |X |language |
| **Fecha, hora y región**: hora larga |sync |X |language |
| **Personalización del escritorio**: tema de escritorio (fondo, color del sistema, sonidos del sistema predeterminados, protector de pantalla) |sync |X |Tema |
| **Personalización del escritorio**: papel tapiz de presentación |sync |X |Tema |
| **Personalización del escritorio**: configuración de la barra de tareas (posición, ocultar automáticamente, etc.) |sync |X |Tema |
| **Personalización del escritorio**: diseño de pantalla de inicio |X |backup | |
| **Dispositivos**: se ha conectado demasiado de impresoras compartidas|X |X |Otros |
| **Explorador de Edge**: lista de lectura |sync |sync |interno |
| **Explorador Edge**: favoritos |sync |sync |interno |
| **Explorador Edge**: sitios principales <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: direcciones URL escritas <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: configuración de la barra de favoritos <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: Mostrar botón Inicio hello <sup> [[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: bloquear elementos emergentes <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: Preguntarme qué toodo con cada descarga <sup> [[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: ofrecer las contraseñas de toosave <sup> [[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: enviar solicitudes de no seguimiento <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: guardar entradas de formularios <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: mostrar sugerencias de búsqueda y de sitios web al escribir <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: preferencias de cookies <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: permitir que los sitios guarden licencias multimedia protegidas en mi dispositivo <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Explorador Edge**: configuración del lector de pantalla <sup>[[1]](#footnote-1)</sup> |sync |sync |interno |
| **Contraste alto**: activar o desactivar |sync |X |Facilidad de acceso |
| **Contraste alto**: configuración de temas |sync |X |Facilidad de acceso |
| **Internet Explorer**: abrir pestañas (dirección URL y título) |sync |sync |Internet Explorer |
| **Internet Explorer**: lista de lectura |sync |sync |Internet Explorer |
| **Internet Explorer**: direcciones URL escritas |sync |sync |Internet Explorer |
| **Internet Explorer**: historial de exploración |sync |sync |Internet Explorer |
| **Internet Explorer**: favoritos |sync |sync |Internet Explorer |
| **Internet Explorer**: direcciones URL excluidas |sync |sync |Internet Explorer |
| **Internet Explorer**: páginas de inicio |sync |sync |Internet Explorer |
| **Internet Explorer**: sugerencias de dominio |sync |sync |Internet Explorer |
| **Teclado**: los usuarios pueden activar o desactivar el teclado en pantalla |sync |X |Facilidad de acceso |
| **Teclado**: activar sí temporal (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Teclado**: activar teclas de filtro (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Teclado**: activar teclas de alternancia (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Internet Explorer**: idioma de dominio: QWERTY chino simplificado - habilitar autoaprendizaje |sync |X |language |
| **Idioma**: QWERTY chino simplificado - habilitar clasificación dinámica del candidato |sync |X |language |
| **Idioma**: QWERTY chino simplificado - juego de caracteres de chino simplificado |sync |X |language |
| **Idioma**: QWERTY chino simplificado - juego de caracteres de chino tradicional |sync |X |language |
| **Idioma**: QWERTY chino simplificado - pinyin aproximado |sync |backup |Idioma |
| **Idioma**: QWERTY chino simplificado - pares aproximados |sync |backup |Idioma |
| **Idioma**: QWERTY chino simplificado - pinyin completo |sync |X |language |
| **Idioma**: QWERTY chino simplificado - pinyin doble |sync |X |language |
| **Idioma**: QWERTY chino simplificado - corrección automática de lectura |sync |X |language |
| **Idioma**: QWERTY chino simplificado - tecla de modificador C/E, MAYÚS |sync |X |language |
| **Idioma**: QWERTY chino simplificado - tecla de modificador C/E, Ctrl |sync |X |language |
| **Idioma**: chino simplificado WUBI - modo de entrada de carácter único |sync |X |language |
| **Idioma**: CHS WUBI - mostrar hello restante de codificación de candidato Hola |sync |X |language |
| **Idioma**: WUBI chino simplificado - pitido cuando la codificación 4 no sea válida |sync |X |Idioma |
| **Idioma**: Bopomofo chino simplificado, incluir CJK Ext-A |sync |X |language |
| **Idioma**: IME japonés - escritura predictiva y palabras personalizadas |sync |sync |language |
| **Idioma**: IME coreano (KOR) |X |X |language |
| **Idioma**: reconocimiento de escritura a mano |X |X |language |
| **Idioma**: perfil de lenguaje |sync |backup |language |
| **Idioma**: corrector ortográfico - autocorrección y resaltar errores ortográficos |sync |backup |language |
| **Idioma**: lista de teclados |sync |backup |language |
| **Pantalla de bloqueo**: toda la configuración de pantalla de bloqueo |X |X | |
| **Lupa**: activar o desactivar (alternancia de maestro) |X |X |Facilidad de acceso |
| **Lupa**: activar o desactivar inversión del color (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Ampliador**: seguimiento - foco de teclado de Hola de seguimiento |sync |X |Facilidad de acceso |
| **Ampliador**: seguimiento - cursor del mouse de Hola de seguimiento |sync |X |Facilidad de acceso |
| **Lupa**: iniciar cuando los usuarios inicien sesión (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Mouse**: cambiar el tamaño de Hola de cursor del mouse |sync |X |otros |
| **Mouse**: cambiar color Hola de cursor del mouse |sync |X |Otros |
| **Mouse**: todas las demás configuraciones |X |X | |
| **Narrador**: inicio rápido |sync |X |Facilidad de acceso |
| **Narrador**: los usuarios pueden cambiar el tono de voz del narrador |sync |X |Facilidad de acceso |
| **Narrador**: los usuarios pueden activar o desactivar las sugerencias de lectura del narrador para los elementos comunes (activado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Narrador**: los usuarios pueden activar o desactivar si pueden oír los caracteres escritos (activado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Narrador**: los usuarios pueden activar o desactivar si pueden oír las palabras escritas (activado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Narrador**: insertar cursor a continuación del narrador (activado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Narrador**: habilitar resaltado visual del cursor del narrador (activado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Narrador**: reproducir indicaciones de sonido (activado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Narrador**: activar las claves en la pantalla táctil hello cuando levante el dedo (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Facilidad de acceso**: establecer Hola grosor del cursor parpadeante Hola |sync |X |Facilidad de acceso |
| **Facilidad de acceso**: quitar imágenes de fondo (desactivado de forma predeterminada) |sync |X |Facilidad de acceso |
| **Encendido y suspensión**: todas las configuraciones |X |X | |
| **Personalización de la pantalla de inicio**: color de acento (solo teléfono). |X |sync |Tema |
| **Escritura**: diccionario ortográfico |sync |backup |language |
| **Escritura**: autocorrección de palabra escrita incorrectamente |sync |backup |language |
| **Escritura**: resaltar palabras incorrectas |sync |backup |language |
| **Escritura**: mostrar sugerencias de texto al escribir |sync |backup |language |
| **Escritura**: agregar un espacio después de seleccionar una sugerencia de texto |sync |backup |language |
| **Escriba**: agregue un punto después de que doble punteo Hola ESPACIADORA |sync |backup |language |
| **Escriba**: poner en mayúscula la primera letra de cada frase de Hola |sync |backup |language |
| **Escritura**: escribir todo en mayúsculas al pulsar dos veces la tecla MAYÚS |sync |backup |language |
| **Escritura**: reproducir sonidos de teclas al escribir |sync |backup |language |
| **Escritura**: datos de personalización para teclado táctil |sync |backup |language |
| **Wi-Fi**: perfiles Wi-Fi (solo WPA) |sync |sync |Contraseñas |

###### <a name="footnote-1"></a>Nota al pie 1
Versión mínima admitida de Windows Creators Update (Build 15063). 

## <a name="related-topics"></a>Temas relacionados
* [Información general de Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitación de Enterprise State Roaming en Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Preguntas más frecuentes sobre itinerancia de datos y configuración](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Configuración de MDM y directivas de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
