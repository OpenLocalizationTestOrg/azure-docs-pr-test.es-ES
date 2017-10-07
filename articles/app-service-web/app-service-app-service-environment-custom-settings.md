---
title: "configuración de aaaCustom para los entornos de servicio de aplicación"
description: "Opciones de configuración personalizada para Entornos del Servicio de aplicaciones"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Opciones de configuración personalizada para Entornos del Servicio de aplicaciones
## <a name="overview"></a>Información general
Porque los entornos del servicio de aplicación están aisladas tooa solo cliente, hay ciertas opciones de configuración que se pueden aplican tooApp exclusivamente los entornos del servicio. Este artículo se explican Hola distintos personalizaciones específicas que están disponibles para entornos del servicio de aplicación.

Si no tiene un entorno de servicio de aplicaciones, consulte [cómo tooCreate un entorno de servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md).

Puede almacenar las personalizaciones del entorno del servicio de aplicaciones mediante el uso de una matriz en hello nueva **clusterSettings** atributo. Este atributo se encuentra en el diccionario de "Propiedades" hello de hello *hostingEnvironments* entidad Azure Resource Manager.

siguiente fragmento de plantilla de administrador de recursos abreviado Hello muestra hello **clusterSettings** atributo:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Hola **clusterSettings** atributo puede incluirse en un Hola de tooupdate de plantilla entorno del servicio de aplicación de administrador de recursos.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Utilice el Explorador de recursos de Azure tooupdate un entorno de servicio de aplicaciones
Como alternativa, puede actualizar Hola entono mediante [Explorador de recursos de Azure](https://resources.azure.com).  

1. En el Explorador de recursos, vaya toohello nodo Hola entono (**suscripciones** > **resourceGroups** > **proveedores**  >  **Microsoft.Web** > **hostingEnvironments**). A continuación, haga clic en Hola entorno específico de servicio de aplicación que desea tooupdate.
2. En el panel derecho de hello, haga clic en **lectura/escritura** en hello superior de la barra de herramientas tooallow interactivo de edición en el Explorador de recursos.  
3. Haga clic en hello azul **editar** plantilla de administrador de recursos de botón toomake Hola editable.
4. Desplazamiento toohello la parte inferior del panel derecho de Hola. Hola **clusterSettings** atributo se encuentra en la parte inferior de hello, donde puede especificar o actualizar su valor.
5. Matriz de Hola de tipo (o copiar y pegar) de los valores de configuración que desee en hello **clusterSettings** atributo.  
6. Haga clic en hello verde **colocar** botón que se encuentra en parte superior de Hola de hello panel derecho toocommit Hola cambio toohello entorno del servicio de aplicaciones.

Sin embargo, enviar cambios de hello, tarda aproximadamente 30 minutos multiplicados por número de Hola de servidores front-end en hello entorno del servicio de aplicación para cambiar tootake efecto de Hola.
Por ejemplo, si un entorno de servicio de aplicaciones tiene cuatro servidores front-end, tardará aproximadamente dos horas para toofinish de actualización de configuración de Hola. Mientras se está implantando el cambio de configuración de hello, no hay otras operaciones de escala o las operaciones de cambio de configuración pueden tener lugar en el entorno del servicio de aplicación Hola.

## <a name="disable-tls-10"></a>Deshabilitación de TLS 1.0
Una pregunta periódica de los clientes, especialmente los clientes que están relacionados con el cumplimiento del estándar PCI auditorías, es cómo tooexplicitly deshabilitar TLS 1.0 para sus aplicaciones.

TLS 1.0 se puede deshabilitar mediante siguiente hello **clusterSettings** entrada:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Cambio del orden del conjunto de aplicaciones de cifrado TLS
Otra cuestión de los clientes es si puede modificar la lista de Hola de cifrado que se negocia entre el servidor y esto puede lograrse mediante la modificación de hello **clusterSettings** tal y como se muestra a continuación. lista de Hola de conjuntos de cifrado disponibles puede obtenerse de [este artículo MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Si se establecen valores incorrectos para los conjuntos de cifrado de hello SChannel no entiende, todos los servidores de tooyour de comunicación TLS podrían dejar de funcionar. En tal caso, será necesario hello tooremove *FrontEndSSLCipherSuiteOrder* entrada de **clusterSettings** y enviar Hola actualiza el Administrador de recursos plantilla toorevert toohello atrás predeterminado cifrado configuración de conjunto.  Utilice esta funcionalidad con precaución.
> 
> 

## <a name="get-started"></a>Primeros pasos
sitio de plantilla de inicio rápido de Azure Resource Manager Hola incluye una plantilla de definición de base de Hola para [crear un entorno de servicio de aplicaciones](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
