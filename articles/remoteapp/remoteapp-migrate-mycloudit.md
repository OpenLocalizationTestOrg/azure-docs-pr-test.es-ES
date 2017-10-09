---
title: "la facturación de hello aaaChange de RemoteApp de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toostop cobrándole de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Migrar desde tooMyCloudIT de Azure RemoteApp 

**¿Actualmente usa Microsoft Azure RemoteApp?** : MyCloudIT creado una herramienta automatizada toomigrate la plataforma de administración de Azure RemoteApp (ARA) colecciones toohello MyCloudIT mientras continúa toorun en Microsoft Azure.

**Aprovechar las ventajas del portal de Azure Resource Manager Hola**: complete la migración en la plataforma de hello MyCloudIT habilita el nuevo portal de Azure Resource Manager del acceso instantáneo tooAzure. Este portal contiene todas las nuevas capacidades de Hola e innovaciones ofrecen por Microsoft Azure, incluyendo acceso tooVirtual máquina tamaños tooensure la implementación se genera necesidades de hello toosupport de su empresa.

**En la solución adecuada de hello tooensure paralelo para satisfacer sus necesidades de pruebas**: herramienta de migración de hello MyCloudIT se integra tooinitiate proceso de migración de Hola y pruebas en paralelo mientras los usuarios actuales de ARA continuar toouse ARA.  Los usuarios permanecerán en ARA hasta que la migración y las pruebas se completen.  herramienta de migración de Hola se integra colección toohandle Hola de ARA típica.  Si cree que tenga un escenario único y no estándar, póngase en contacto con nosotros en [ sales@conexlink.com ](mailto:sales@conexlink.com) para que podamos proporcionar un tooassist plan diseñados con la migración.

**Capacidades de escritorio como servicio**: tenga en cuenta que MyCloudIT no solo ofrece capacidades de RemoteApp de hello está acostumbrado a, pero también le ofrecemos servicios de escritorio como un completo capacidades para hello igual costo al mes sin que ningún usuario mínimo requisitos.

## <a name="what-we-will-do-for-you"></a>Lo que haremos por usted

MyCloudIT automatiza la migración de saludo de la plantilla de RemoteApp de Azure desde el portal de Azure clásico de Hola de su Portal de administrador de recursos de Azure de su suscripción con nuestra herramienta de migración automática de toohello de suscripción.  

> [!NOTE]
> Hola a Hello Azure RemoteApp plantilla debe permanecer en la misma región de Azure que su implementación de Azure RemoteApp original.  Si necesita toochange regiones de Azure o suscripciones de Azure durante la migración de hello, póngase en contacto con nosotros para obtener orientación adicional en [ sales@conexlink.com ](mailto:sales@conexlink.com).

Lea a continuación para obtener información detallada en el proceso de migración de hello automatizada con hello MyCloudIT la herramienta de migración:

1. herramienta de migración de Hello examina sus suscripciones actuales para todas las implementaciones de ARA existentes.  
2. Seleccionar un ARA colección toomigrate a la vez.  Si tiene varias colecciones, ejecute la herramienta varias veces.
3. Dispone de hello opción toocopy Hola discos de perfil de usuario (UPD) tooyour nueva implementación por lo que puede recuperar los datos heredados, o asignar manualmente la UPD toohello nueva implementación. Si elige toocopy su UPD, se ahorrará UPD hello e incluyen un archivo de texto que se asigna nombre hello UPD nombre tooeach los usuarios.  Hola UPD será recurso compartido de tooa copiado en el servidor de hello RDSMGMT `F:\Shares\LegacyUPD` y se expondrá a través de recurso compartido de hello `\\RDSmgmt\LegacyUPD`. 
4. La migración no producirá tiempo de inactividad para la implementación de ARA actual.  Sin embargo, si se realizan cambios toohello UPD (de ARA) después de la copia de hello, estos cambios no se reflejarán en UPD Hola almacenados en el portal de Azure Resource Manager Hola. 
5. Si tiene máquinas virtuales adicionales como controladores de dominio y servidores de archivos en la red Virtual de Azure clásico se establecerán entre existente clásico red Virtual de Azure de emparejamiento de VNet y hello nueva red Virtual se creará para usted, en Hola nuevo recurso de Azure Portal de administrador.
6. Nuestra solución automatizada solo establecerá entre existente clásico red Virtual de Azure de emparejamiento de VNet y Hola nueva red Virtual si la implementación de ARA existente es una implementación híbrida; es decir, se autentican con un controlador de dominio de directorio activo de Windows Server en hello existente clásico de red Virtual. Si no se establecer para la colección de emparejamiento de VNet, pero requieren de emparejamiento de VNet, póngase en contacto con nosotros como [ sales@conexlink.com ](mailto:sales@conexlink.com) estaremos encantado tooconfigure emparejamiento de red virtual sin ningún costo adicional.
7. Nuestra solución automatizada garantizará que se actualiza la configuración de DNS de Azure con hello tooensure de configuración de red Virtual nueva, la nueva implementación puede conectarse tooyour existente de controlador de dominio en hello clásico red virtual.
8. Nuestra solución automatizada se asegurará de que no hay ningún conflicto de dirección IP cuando se crea esta nueva red Virtual y establecer el emparejamiento de red virtual de Hola para las implementaciones con un servidor directorio activo de Windows Server existente.
9. Si solo usa Azure AD para la autenticación, MyCloudIT creará un nuevo Windows servidor de dominio de Active Directory y utilice usuarios de Azure AD Connect toosynchronize entre la instancia existente de Azure AD de Hola y Hola que crea el dominio de nuevo Windows Server Active Directory por MyCloudIT.
10. Si usas un usuario de dominio de Active Directory de Windows Server tooauthenticate ARA, nuestra solución automatizada conectará el nuevo tooyour de implementación de MyCloudIT existente de controlador de dominio de Active Directory de Windows Server a través de intercambio de tráfico de red virtual.
11. Si usa Azure Active Directory Domain Services para la autenticación también podemos realizar la migración, pero debe ponerse en contacto con nosotros para que creemos un plan de migración personalizado.  Envíe un correo electrónico[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Una vez migrado el Hola colección toobe está confirmado, póngase cómodo y relájese mientras nuestra solución automatizada migra su colección de ARA y discos de perfil de usuario (opcional) toohello nueva aplicaciones remotas MyCloudIT controlada por solución.
13. Una vez completada la implementación de hello, volver a publicaremos Hola mismas aplicaciones que se publicaron en ARA y tras la implementación estará toopublish capaz de otras aplicaciones.

## <a name="post-migration-benefits"></a>Ventajas tras la migración

1. Proporcionamos Hola management console que permite toomanage Hola completa del ciclo de vida de la implementación de aplicaciones remotas.
2. Es posible que pueda toomanage su Virtual máquinas de nuestro portal.  Inicie, detenga y cambie el tamaño de las máquinas virtuales si es necesario.
3. consola de administración de Hello proporciona Hola toocreate de capacidad y administrar los usuarios / grupos desde el portal de administración.
4. consola de administración de Hello proporciona a los usuarios de hello capacidad toosynchronize con Office 365 toocreate una misma experiencia de inicio de sesión.
5. consola de administración Hello proporciona Hola capacidad toocreate aplicación remota adicionales y colecciones de escritorio sin costes de usuario duplicados o los requisitos mínimos de usuario. 
6. consola de administración de Hello proporciona capacidad de hello toopublish nuevas aplicaciones de aplicaciones remotas.
7. consola de administración de Hello proporciona inicio de hello capacidad tooschedule Hola y el cierre de la implementación de aplicaciones remotas si solo necesita la solución durante unas horas específicas.
8. consola de administración de Hello proporciona la instalación de hello capacidad tooautomate hello y la configuración de agente de copia de seguridad de Azure de Hola que proporciona un historial de retención de documento para los datos de clientes.
9. consola de administración de Hello proporciona métricas de tooperformance de acceso de la implementación.  Esto deja Hola capacidad tooidentify los posibles cuellos de botella de rendimiento sin necesidad de instalar herramientas de administración de rendimiento adicionales.
10. Si tienes varios hosts de sesión, será capaz de tooenable Autoescala sesión de Hola para que solamente se ejecutan los hosts que necesiten toobe ejecutando.
11. MyCloudIT proporciona el servidor de puerta de enlace de acceso toohello RDWeb a través de un nombre de dominio MyCloudIT.  También proporcionamos Hola capacidad toore mapa Hola URL tooa dirección URL personalizada para personalización de marca del usuario final.

## <a name="prerequisites-for-migration"></a>Requisitos previos para la migración

1. Debe tener acceso toohello suscripción de Azure que hospeda la solución actual de Azure RemoteApp.
2. Debe conceder nuestro portales permisos dentro de su suscripción toomigrate la plantilla y toocreate / modificar la nueva implementación de MyCloudIT.
3. Tenga en cuenta que debido tooa limitación en la aplicación de Azure remota, cada colección solo se puede migrar tres veces.  Si necesita una colección de toomigrate más de tres veces, puede generar un tooincrease de tooAzure vale su recuento de exportación, o póngase en contacto con nosotros y se le ayudará en número de exportación de hello ARA solicitudes tooincrease Hola.

## <a name="mycloudit-billing"></a>Facturación de MyCloudIT

Vea [MyCloudIT precios para soluciones de RemoteApp](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) para obtener información acerca de cómo toopredict y administrar los costos generales de Azure.

Si todavía tiene alguna pregunta, póngase en contacto con nosotros en [ sales@conexlink.com ](mailto:sales@conexlink.com) o ver vídeo de demostración completa de hello [herramienta de migración de Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

