---
title: aaaSecurity centrales de notificaciones
description: En este tema se explica la seguridad de los Centros de notificaciones de Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Seguridad
## <a name="overview"></a>Información general
Este tema describe el modelo de seguridad de Hola de centros de notificaciones de Azure. Dado que los centros de notificaciones son una entidad de Bus de servicio, que implementan Hola mismo modelo de seguridad que Service Bus. Para obtener más información, vea hello [autenticación del Bus de servicio](https://msdn.microsoft.com/library/azure/dn155925.aspx) temas.

## <a name="shared-access-signature-security-sas"></a>Seguridad de Firma de acceso compartido (SAS)
Los Centros de notificaciones implementan un esquema de seguridad de nivel de entidad llamado SAS (Firma de acceso compartido). Este esquema permite mensajería toodeclare entidades too12 reglas de autorización en su descripción que conceden derechos en dicha entidad.

Cada regla contiene un nombre, un valor de clave (secreto compartido) y un conjunto de derechos, como se explica en la sección de Hola "Notificaciones de seguridad". Cuando se crea un centro de notificaciones, automáticamente se crean dos reglas: una con derechos de escucha (que Hola usos de la aplicación de cliente) y otra con todos los derechos (que Hola aplicación back-end utiliza).

Al realizar la administración de registros desde aplicaciones cliente, si la información de Hola se envía a través de notificaciones no es importante (por ejemplo, las actualizaciones de tiempo), un tooaccess de forma habitual un centro de notificaciones es clave-valor hello toogive de hello regla acceso de solo escucha toohello aplicación de cliente y valor de clave de hello toogive de hello regla acceso completo toohello aplicación back-end.

No se recomienda que incrustar clave-valor hello en aplicaciones de cliente de la tienda Windows. Un tooavoid de manera incrustar clave-valor hello es aplicación de cliente hello toohave recuperarlo de backend de la aplicación hello en el inicio.

Es importante toounderstand que Hola clave con acceso de escucha permite que un cliente tooregister de aplicación para cualquier etiqueta. Si la aplicación debe restringir a los clientes de etiquetas toospecific toospecific de registros (por ejemplo, cuando las etiquetas representan identificadores de usuario), el back-end de aplicación debe realizar registros Hola. Para obtener más información, consulte Administración de registros. Tenga en cuenta que, de esta manera, aplicación de cliente de hello no tendrá acceso directo tooNotification concentradores.

## <a name="security-claims"></a>Notificaciones de seguridad
Entidades tooother similar, se permiten las operaciones del centro de notificaciones para tres notificaciones de seguridad: escuchar, enviar y administrar.

| Notificación | Descripción | Operaciones permitidas |
| --- | --- | --- |
| Escuchar |Crear o actualizar, leer y eliminar registros únicos |Crear o actualizar registro<br><br>Leer el registro<br><br>Leer todos los registros de un controlador<br><br>Eliminar registro |
| Los métodos Send |Centro de notificaciones de toohello de mensajes de envío |Enviar mensaje |
| Manage |CRUD en los Centros de notificaciones (incluida la actualización de las credenciales de PNS y claves de seguridad) y registros de lectura basados en etiquetas |Crear/Actualizar/Eliminar Centros de notificaciones<br><br>Leer registros por etiqueta |

Los centros de notificaciones aceptan notificaciones concedidas por tokens de Control de acceso de Microsoft Azure y tokens de firma generados con claves compartidas configuradas directamente en hello centro de notificaciones.

