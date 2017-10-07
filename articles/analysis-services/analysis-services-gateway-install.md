---
title: puerta de enlace de datos de aaaInstall local | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar una puerta de enlace de datos local."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Instalación y configuración de una puerta de enlace de datos local
Se requiere una puerta de enlace de datos local cuando uno o varios servidores de servicios de análisis de Azure en Hola mismo región conectarse a orígenes de datos locales de tooon. toolearn más información acerca de la puerta de enlace de hello, consulte [puerta de enlace de datos local](analysis-services-gateway.md).

## <a name="prerequisites"></a>Requisitos previos
**Requisitos mínimos:**

* .NET Framework 4.5
* versión de 64 bits de Windows 7 o Windows Server 2008 R2 (o posterior)

**Se recomienda que use:**

* CPU de 8 núcleos
* 8 GB de memoria
* versión de 64 bits de Windows 2012 R2 (o posterior)

**Consideraciones importantes:**

* Durante la instalación, al registrar la puerta de enlace con Azure, se selecciona región predeterminados de Hola para su suscripción. Puede elegir otra región. Si tiene servidores en varias regiones, debe instalar una puerta de enlace en cada una de ellas. 
* no se puede instalar la puerta de enlace de Hello en un controlador de dominio.
* Solo se puede instalar una puerta de enlace en un equipo.
* Instalar la puerta de enlace de hello en un equipo que permanece en y no queda toosleep.
* No instale la puerta de enlace de hello en un equipo de la red de forma inalámbrica conectado tooyour. Puede disminuir el rendimiento.


## <a name="download"></a>Descarga
 [Descargar la puerta de enlace de Hola](https://aka.ms/azureasgateway)

## <a name="install"></a>Instalación

1. Ejecute la configuración.

2. Seleccione una ubicación, acepte los términos de Hola y, a continuación, haga clic en **instalar**.

   ![Ubicación de instalación y términos de la licencia](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Seleccione **Puerta de enlace de datos local (se recomienda)**. Azure Analysis Services no admite el modo personal.

   ![Elección del tipo de puerta de enlace](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Escriba una cuenta toosign en tooAzure. cuenta de Hello debe estar en de Azure Active Directory su inquilino. Esta cuenta se usa para el Administrador de puerta de enlace de Hola. 

   ![Escriba una cuenta toosign en tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Si inicia sesión con una cuenta de dominio, será asignado tooyour de cuenta profesional en Azure AD. Se utilizará la cuenta de su organización como administrador de puerta de enlace de Hola Hola.

## <a name="register"></a>Registro
En orden toocreate un recurso de puerta de enlace de Azure, debe registrar instancia local de hello instalada con hello puerta de enlace de servicio en la nube. 

1.  Seleccione **Registrar una nueva puerta de enlace en este equipo**.

    ![Registro](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Escriba el nombre y la clave de recuperación de la puerta de enlace. De forma predeterminada, la puerta de enlace de hello usa región predeterminados de la suscripción. Si necesita tooselect una región distinta, seleccione **cambiar región**.

   ![Registro](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Creación de un recurso de puerta de enlace de Azure
Una vez que ha instalado y registrado la puerta de enlace, deberá toocreate un recurso de puerta de enlace en su suscripción de Azure. Inicie sesión en tooAzure con hello misma cuenta que usó al registrar la puerta de enlace de Hola.

1. En Azure Portal, haga clic en **Crear un nuevo servicio** > **Enterprise Integration** > **Puerta de enlace de datos local** > **Crear**.

   ![Creación de un recurso de puerta de enlace](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. En **Crear puerta de enlace de conexión**, escriba estos valores:

    * **Nombre**: escriba un nombre para el recurso de puerta de enlace. 

    * **Suscripción**: seleccione Hola tooassociate de suscripción de Azure con su recurso de puerta de enlace. 
    Esta suscripción debe ser Hola misma suscripción que los servidores están en.
   
      suscripción de Hello predeterminada se basa en hello cuenta de Azure que usan toosign en.

    * **Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.

    * **Ubicación**: región Hola seleccione registrado la puerta de enlace.

    * **Nombre de la instalación**: si la instalación de puerta de enlace no está seleccionada, la puerta de enlace de hello seleccione registrado. 

    Cuando haya terminado, haga clic en **Crear**.

## <a name="connect-servers"></a>Conectarse a recursos de puerta de enlace de toohello de servidores

1. En la introducción al servidor de Azure Analysis Services, haga clic en **Puerta de enlace de datos local**.

   ![Conectar a servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. En **elegir una puerta de enlace de datos de On-Premises tooconnect**, seleccione el recurso de puerta de enlace y, a continuación, haga clic en **conectar la puerta de enlace seleccionado**.

   ![Conectarse a recursos de servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Si la puerta de enlace no aparece en la lista de hello, el servidor es probable que no está en Hola la misma región como región Hola que especificó al registrar la puerta de enlace de Hola. 

Eso es todo. Si necesita tooopen puertos o realice cualquier solución de problemas, que seguro toocheck out [puerta de enlace de datos local](analysis-services-gateway.md).

## <a name="next-steps"></a>Pasos siguientes
* [Administración de Analysis Services](analysis-services-manage.md)   
* [Obtención de datos de Azure Analysis Services](analysis-services-connect.md)
