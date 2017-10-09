---
title: un proyecto de servicio de nube de Azure con Visual Studio aaaCreating | Documentos de Microsoft
description: "Obtenga información acerca de toocreate ahora un proyecto de servicio de nube de Azure con Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Creación de un proyecto de servicio en la nube de Azure con Visual Studio
Hello Azure Tools para Visual Studio proporciona una plantilla de proyecto que le permite crear un servicio de nube de Azure. Una vez que se ha creado el proyecto de hello, Visual Studio le permite tooconfigure, depurar e implementar tooAzure de servicio de nube de Hola.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Pasos toocreate un proyecto de servicio de nube de Azure en Visual Studio
En esta sección se le enseñará cómo crear un proyecto de servicio en la nube de Azure en Visual Studio con uno o más roles web.  

1. Inicie Visual Studio como administrador.

1. En el menú principal de hello, seleccione **archivo** > **New** > **proyecto**.

1. Seleccione **nube** desde Hola Visual C# o Visual Basic nodos de la plantilla de proyecto y seleccione **servicio de nube de Azure** de lista de Hola de plantillas.

    ![Nuevo servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Especifique qué versión de Hola desea toouse toodevelop el proyecto de .NET Framework.

1. Escriba un nombre y una ubicación para el proyecto y un nombre para la solución de Hola. 

1. Seleccione **Aceptar**.

1. Hola **nuevo servicio de nube de Microsoft Azure** cuadro de diálogo, roles de hello select que desee tooadd y elija tooadd de botón de flecha derecha Hola ellos tooyour solución.

    ![Selección de nuevos roles de servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. un rol que se ha agregado al mantener el mouse en función del Hola Hola toorename **nuevo servicio de nube de Microsoft Azure** cuadro de diálogo y, en el menú contextual de hello, seleccione **cambiar el nombre de**. También puede cambiar el nombre un rol dentro de la solución (Hola **el Explorador de soluciones**) después de que se ha agregado.

    ![Cambio de nombre de rol de servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

proyecto de Azure en Visual Studio Hello tiene proyectos de rol toohello asociaciones de solución de Hola. proyecto de Hello también incluye hello *archivo de definición de servicio* y *archivo de configuración de servicio*:

- **Archivo de definición de servicio** -define los valores de tiempo de ejecución de Hola para su aplicación, incluidos los roles son necesarios, los puntos de conexión y el tamaño de máquina virtual. 
- **Archivo de configuración de servicio** -configura el número de instancias de un rol se ejecuta y Hola valores de los valores de hello definidos para un rol. 

Para obtener más información acerca de estos archivos, consulte [configurar Roles de Hola para un servicio de nube de Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Pasos siguientes
- [Administración de roles en los proyectos de servicio en la nube de Azure con Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
