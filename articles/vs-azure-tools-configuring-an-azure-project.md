---
title: un proyecto de servicio de nube de Azure con Visual Studio aaaConfigure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure un Azure en la nube de proyecto de servicio en Visual Studio, dependiendo de los requisitos para ese proyecto."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Configuración de un proyecto de servicio en la nube de Azure con Visual Studio
Es posible configurar un proyecto de servicio en la nube de Azure dependiendo de los requisitos para dicho proyecto. Puede establecer propiedades de proyecto de Hola para hello siguientes categorías:

- **Publicar un tooAzure de servicio de nube** -puede establecer un toomake propiedad seguro de que no se elimina accidentalmente un tooAzure de servicio implementado en la nube existente.
- **Ejecutar o depurar un servicio de nube en el equipo local de hello** -puede seleccionar una toouse de configuración de servicio e indicar si desea que el emulador de almacenamiento de Azure de toostart Hola.
- **Validar un paquete de servicios de nube cuando se crea** -puede decidir tootreat las advertencias como errores, por lo que puede garantizar ese paquete de servicio de nube de hello implementa sin problemas. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Pasos tooconfigure un proyecto de servicio de nube de Azure
1. Abra o cree un proyecto de servicio en la nube en Visual Studio.

1. En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **propiedades**.
   
1. En la página de propiedades del proyecto de hello, seleccione hello **desarrollo** ficha.

    ![Menú Propiedades del proyecto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Establecer **Preguntar antes de eliminar una implementación existente** demasiado**True**. Esta configuración permite a tooensure no elimina accidentalmente una implementación existente en Azure

1. Seleccione Hola deseado **configuración del servicio** tooindicate configuración de servicio que desee toouse al ejecutar o depurar su servicio en la nube localmente. Para obtener más información acerca de cómo toomodify una configuración del servicio para un rol, consulte [cómo roles de hello tooconfigure para un Azure servicio en la nube con Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Establecer **emulador de almacenamiento de Azure iniciar** demasiado**True** toostart Hola emulador de almacenamiento Azure al ejecutar o depurar su servicio en la nube localmente.

1. Establecer **tratar advertencias como errores** demasiado**True** toomake seguro de que no se puede publicar si hay errores de validación de paquetes.

1. Establecer **usar puertos de proyecto web** demasiado**True** toomake seguro de que su rol web usa Hola mismo puerto cada vez que se inicia localmente en IIS Express.

1. En la barra de herramientas de Visual Studio hello, seleccione **guardar**.

## <a name="next-steps"></a>Pasos siguientes
- [Configuración de un proyecto de Azure mediante varias configuraciones de servicio](vs-azure-tools-multiple-services-project-configurations.md)

