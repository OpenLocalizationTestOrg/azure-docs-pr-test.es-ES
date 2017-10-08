---
title: "aaaWeb la clonación de la aplicación mediante el Portal de Azure"
description: "Obtenga información acerca de cómo tooclone su toonew de aplicaciones Web aplicaciones Web mediante el Portal de Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante el Portal de Azure
característica de clonación de Hello [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) permite fácilmente clonar aplicación web existente aplicaciones tooa recién creado en una región diferente o en Hola la misma región. Esto le permitirá clientes toodeploy un número de aplicaciones en diferentes regiones rápida y fácilmente.

La clonación de aplicaciones actualmente solo se admite para los planes de Servicio de aplicaciones de nivel Premium. los usos de característica nuevos Hola Hola mismo limitaciones como característica de copia de seguridad de aplicaciones Web, consulte [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Clonación de una aplicación existente
debe estar ejecutando la aplicación web de Hello en hello **Premium** modo en orden para toocreate un clon de la aplicación web de Hola.

1. Hola [Portal de Azure](https://portal.azure.com/), abra la hoja de la aplicación web.
2. Haga clic en **Herramientas**. A continuación, en hello **herramientas** hoja, haga clic en **clonar aplicación**.
   
    ![][1]
   
   > [!NOTE]
   > Si hello web app no está ya en hello **Premium** modo, recibirá un mensaje que indica los modos de hello compatible para la clonación de la aplicación. En este punto, tiene Hola opción tooselect **actualizar**.
   > 
   > 
3. Hola **clonar aplicación** hoja proporcione un nombre de aplicación web nueva de hello, grupo de recursos y Plan de servicio de aplicaciones. También Hola usuario será capaz de toochoose si tooclone varias opciones de configuración de aplicación web de origen o no.
   
    ![][2]
4. Después de hacer clic **crear** plataforma Hola comenzará a funcionar sobre la creación de un clon de la aplicación web de origen de Hola.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Clonar un tooan de aplicación existente entorno del servicio de aplicaciones
Hola **clonar aplicación** hoja Hola cliente tendrá la Hola opción toochoose un grupo de aplicaciones en un entorno de servicio de aplicación existente.

## <a name="current-restrictions"></a>Restricciones actuales
Esta característica está actualmente en vista previa, estamos trabajando tooadd nuevas capacidades con el tiempo, Hola lista siguiente se Hola restricciones conocidas de compatibilidad actual de Hola de clonación de la aplicación de Portal de Azure:

* No se clona la configuración del Administrador de tráfico de Azure.
* No se clona la configuración de escalado automático.
* No se clona la configuración de programación de copia de seguridad.
* No se clona la configuración de red virtual.
* Detalles de aplicaciones no se establecen automáticamente en la aplicación web de destino de Hola
* No se clona la configuración de Easy Auth.
* No se clona la extensión Kudu.
* No se clonan las reglas de TiP.
* No se clona el contenido de la base de datos

### <a name="references"></a>Referencias
* [Clonación de aplicaciones web con PowerShell](app-service-web-app-cloning.md)
* [Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-backup.md)
* [¿Cómo tooCreate un entorno de servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md)
* [Creación de una aplicación web en un entorno del Servicio de aplicaciones](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
