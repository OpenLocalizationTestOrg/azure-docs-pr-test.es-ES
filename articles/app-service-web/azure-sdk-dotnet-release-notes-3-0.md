---
title: SDK para .NET 3.0 notas aaaAzure | Documentos de Microsoft
description: "Notas de la versión de SDK de Azure para .NET 3.0"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Notas de la versión de SDK de Azure para .NET 3.0

Este tema incluye notas de la versión con la versión 3.0 de hello Azure SDK para. NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Resumen de la versión de SDK de Azure para .NET 3.0

Fecha de lanzamiento: 07/03/2017
 
No toohello de cambios de separación de Azure SDK 3.0 se han introducido en esta versión. No hay también ninguna tooleverage del proceso de actualización necesitado este SDK con proyectos de servicio en la nube existentes. uso de tooallow de hello Azure SDK 3.0 sin necesidad de un proceso de actualización, Azure SDK 3.0 instala toohello mismos directorios que Azure SDK 2.9. Mayoría de los componentes de hello no ha cambiado la versión principal de Hola de 2.9 pero en su lugar acaba de actualizar número de compilación de Hola.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- En Visual Studio de 2017, esta versión de hello Azure SDK para .NET se basa en toohello carga de trabajo de Azure. Todas las herramientas de hello necesita toodo desarrollo de Azure va a formar parte de Visual Studio de 2017 en el futuro. Para Visual Studio 2015 Hola SDK estará disponible a través de WebPI. Se ha suspendido el SDK de Azure para las versiones de .NET para Visual Studio 2013 ahora que se publicado Visual Studio 2017.

### <a name="azure-diagnostics"></a>Diagnóstico de Azure

- Hola modificada comportamiento tooonly almacenar una cadena de conexión parcial con clave de hello reemplazado por un token de cadena de conexión de almacenamiento de información de diagnóstico de servicios en la nube. clave de almacenamiento real de Hola ahora se almacena en la carpeta de perfil de usuario de hello, por lo que se puede controlar el acceso. Visual Studio leerá clave de almacenamiento de Hola de carpeta de perfil de usuario para la depuración local y el proceso de publicación. 
- En cambio toohello de respuesta se ha descrito anteriormente, Visual Studio Online team Hola mejorada plantilla de tarea de implementación de servicios de nube de Azure para que los usuarios especificar clave de almacenamiento de Hola para establecer la extensión de diagnóstico al publicar tooAzure de integración continua y la implementación.
- Que hemos hecho posible toostore cadena de conexión segura y tokenización para diagnósticos de Azure (WAD), toohelp solucionar problemas con la configuración entre entornos.
 
### <a name="windows-server-2016-virtual-machines"></a>Máquinas virtuales Windows Server 2016

- Visual Studio ahora admite la implementación de servicios en la nube de tooOS máquinas virtuales de familia 5 (Windows Server 2016). Para los servicios de nube existente, puede cambiar su configuración tootarget Hola nueva familia del SO. Al crear nuevos servicios de nube, si decide que el servicio de hello toocreate mediante .net 4.6 o posterior, serán Hola servicio toouse 5 de la familia de SO.  Para obtener más información, puede revisar hello [familia del SO invitado compatible con la tabla](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Problemas conocidos

- El SDK de Azure para .NET 3.0 provoca un problema cuando se quita Visual Studio 2017 en una configuración en paralelo con Visual Studio 2015.  Si tienes hello Azure SDK instalado para Visual Studio 2015, Hola emulador de almacenamiento de Microsoft Azure y el emulador de proceso de Azure de Microsoft se quitarán si desinstala Visual Studio de 2017.  Esto generará un error al crear y depurar nuevos proyectos de servicios en la nube en Visual Studio 2015. En Ordenar toofix este problema, vuelva a instalar hello Azure SDK de hello instalador de plataforma Web.  Hello problema se solucionará en una futura actualización de Visual Studio de 2017.  .

 
### <a name="azure-in-role-cache"></a>Caché en rol de Azure 

- La compatibilidad con Azure In-Role Cache finalizó el 30 de noviembre de 2016. Para más detalles, haga clic [aquí](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




