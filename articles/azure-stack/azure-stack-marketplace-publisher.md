---
title: aaaUse Hola toocreate del Kit de herramientas de Marketplace y publicar elementos de marketplace | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooquickly crear elementos de marketplace con hello Kit de herramientas de publicación"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a>Agregar elementos de Marketplace con la herramienta de publicación
Agregar el contenido toohello [Azure Marketplace de pila](azure-stack-marketplace.md) hace que su tooyou disponibles de soluciones y los inquilinos para la implementación.  Hola Kit de herramientas de Marketplace crea archivos de paquetes de Azure Marketplace (.azpkg) basados en plantillas del Administrador de recursos de Azure IaaS o extensiones de máquina virtual.  También puede usar archivos de hello Kit de herramientas de Marketplace toopublish .azpkg, creado con la herramienta de Hola o mediante [manual](azure-stack-create-and-publish-marketplace-item.md) pasos.  En este tema le guía por descargar herramienta hello, creación de un elemento de marketplace basado en una plantilla de máquina virtual y, a continuación, publicar ese toohello elemento Azure Marketplace de pila.     


## <a name="prerequisites"></a>Requisitos previos
 - Debe ejecutar el Kit de herramientas de hello en el host de la pila de Azure de Hola o tener [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) conectividad de la máquina de Hola donde se ejecuta la herramienta de Hola.

 - Descargar hello [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) y extraer.

 - Descargar hello [herramienta de empaquetado de la Galería de Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe). 

 - Publicar toohello marketplace requiere iconos y un archivo en miniatura.  Puede utilizar su propia o guardar hello [ejemplo](azure-stack-marketplace-publisher.md#support-files) archivos localmente en este ejemplo.

## <a name="download-hello-tool"></a>Descargar la herramienta de Hola
Hello Kit de herramientas de Marketplace puede ser [descargado desde el repositorio de herramientas de la pila de Azure de hello](azure-stack-powershell-download.md).


##  <a name="create-marketplace-items"></a>Crear elementos de Marketplace
En esta sección, utilice Hola Kit de herramientas de Marketplace toocreate un paquete de elemento de marketplace en formato .azpkg.  

### <a name="provide-marketplace-information-with-wizard"></a>Proporcionar información de Marketplace con el Asistente
1. Ejecute hello Kit de herramientas de Marketplace desde una sesión de PowerShell:
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. Haga clic en hello **solución** ficha.  Esta pantalla acepta información sobre el elemento de Marketplace. Escriba información sobre el elemento como se desee tooappear en marketplace Hola.  También puede especificar un [archivo de parámetros](azure-stack-marketplace-publisher.md#use-a-parameters-file) formulario de hello tooprepopulate.  
    
    ![captura de pantalla de la primera pantalla del kit de herramientas de Marketplace](./media/azure-stack-marketplace-publisher/image7.png)
3. Haga clic en **Examinar** y seleccione un archivo de imagen para cada campo de icono y captura de pantalla.  Puede utilizar sus propios iconos u Hola iconos de ejemplo Hola [archivos auxiliares](azure-stack-marketplace-publisher.md#support-files) sección.
4. Una vez que se rellenan todos los campos, seleccione "Vista previa de la solución" para una vista previa de la solución de hello dentro de hello Marketplace.  Puede revisar y editar texto hello, imágenes y captura de pantalla antes de hacer clic **siguiente**.  

### <a name="import-template-and-create-package"></a>Importar la plantilla y crear el paquete
En esta sección, importar plantilla hello y trabajar con entradas de la solución.

1.  Haga clic en **examinar** y seleccione hello *azuredeploy.json* desde la carpeta de 101-Simple-VM de Windows hello en hello descargar plantillas.

    ![captura de pantalla de la segunda pantalla del kit de herramientas de Marketplace](./media/azure-stack-marketplace-publisher/image8.png)
2.  Asistente para la implementación Hello se rellena una con un *básica* elementos de paso y entrada para cada parámetro especificado en la plantilla de Hola.  Puede agregar pasos adicionales y mover entradas entre pasos.  Por ejemplo, puede que quiera pasos “Configuración de front-end” y “Configuración de back-end” para la solución.
3.  Especifique Hola ruta de acceso tooAzureGalleryPackager.exe.  
4.  Haga clic en **crear** y Hola Kit de herramientas de Marketplace empaqueta la solución en un archivo .azpkg.  Una vez que haya finalizado, el Asistente de hello muestra archivo de solución de tooyour de ruta de acceso de Hola y conceda a Hola toocontinue opción publicar su pila tooAzure de paquete.


## <a name="publish-marketplace-items"></a>Publicar elementos de Marketplace
En esta sección, publicar Hola marketplace elemento tooyour Azure Marketplace de pila.

![captura de pantalla de la primera pantalla del kit de herramientas de Marketplace](./media/azure-stack-marketplace-publisher/image9.png)

1.  Asistente de Hello requiere información toopublish la solución:
    
    |Campo|Descripción|
    |-----|-----|
    | Service Admin Name (Nombre del administrador de servicios) | Cuenta del administrador del servicio  Ejemplo: ServiceAdmin@mydomain.onmicrosoft.com |
    | Password | Contraseña de cuenta del administrador de servicios. |
    | Punto de conexión de API | Punto de conexión de Azure Resource Manager de Azure Stack.  Ejemplo: management.local.azurestack.external |
2.  Haga clic en **publicar** y se muestra el registro de hello de publicación.
3.  Se está toodeploy ahora se puede el elemento publicado a través del portal de Azure pila Hola.


## <a name="use-a-parameters-file"></a>Usar un archivo de parámetros
También puede utilizar un archivo toocomplete Hola marketplace elemento información de parámetros de.  

Hello Marketplace Kit de herramientas incluye un *solution.parameters.ps1* toocreate puede utilizar su propio archivo de parámetros.


## <a name="support-files"></a>Archivos auxiliares
| Descripción | Muestra |
| ----- | ----- |
| Icono .png de 40 × 40 | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| Icono .png de 90 × 90 | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| Icono .png de 115 × 115 | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| Icono .png de 255 × 115 | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| Vista en miniatura .png de 533 × 324 | ![](./media/azure-stack-marketplace-publisher/image5.png) |


