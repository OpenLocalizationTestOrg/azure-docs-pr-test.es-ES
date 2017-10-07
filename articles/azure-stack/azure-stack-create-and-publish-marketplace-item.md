---
title: aaaCreate y publicar un elemento de Marketplace en pila de Azure | Documentos de Microsoft
description: Cree y publique un elemento de Marketplace en Azure Stack.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 77e5f60c-a86e-4d54-aa8d-288e9a889386
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: erikje
ms.openlocfilehash: 6f6a7af96f9d8de9098ac7eee4ba2ac9bc3d6a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-publish-a-marketplace-item"></a>Creación y publicación de un producto en Marketplace
## <a name="create-a-marketplace-item"></a>Creación de un elemento para Marketplace
1. [Descargar](http://www.aka.ms/azurestackmarketplaceitem) herramienta Empaquetador de galería de Azure de Hola y elemento de Azure Marketplace de pila de ejemplo de Hola.
2. Abrir elemento de catálogo de soluciones de ejemplo de Hola y cambie el nombre hello **SimpleVMTemplate** carpeta. (Hola uso mismo nombre como el elemento de Marketplace: por ejemplo, **Contoso.TodoList**.) Esta carpeta contiene:
   
       /Contoso.TodoList/
       /Contoso.TodoList/Manifest.json
       /Contoso.TodoList/UIDefinition.json
       /Contoso.TodoList/Icons/
       /Contoso.TodoList/Strings/
       /Contoso.TodoList/DeploymentTemplates/
3. [Cree una plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) o elija una de GitHub. elemento de Marketplace de Hello usa este toocreate un recurso de plantilla.
4. toomake seguro de que el recurso de Hola pueden implementarse correctamente, probar plantilla Hola con hello las API de pila de Microsoft Azure.
5. Si la plantilla se basa en una imagen de máquina virtual, siga las instrucciones de hello demasiado[agregar un tooAzure de imagen de máquina virtual pila](azure-stack-add-vm-image.md).
6. Guarde la plantilla de administrador de recursos de Azure en hello **/Contoso.TodoList/DeploymentTemplates/** carpeta.
7. Elija los iconos de Hola y texto para el elemento de Marketplace. Agregar iconos toohello **iconos** carpeta y agregar texto toohello **recursos** archivo Hola **cadenas** carpeta. Usar hello pequeño, mediano, grande y toda la convención de nomenclatura para los iconos. Consulte la sección [Referencia de UI del elemento de Marketplace](#reference-marketplace-item-ui) para obtener una descripción detallada.
   
   > [!NOTE]
   > Todos los tamaños de icono cuatro (pequeño, mediano y grande, todo) son necesarios para generar el elemento de Marketplace de hello correctamente.
   > 
   > 
8. Hola **manifest.json** de archivos, cambiar **nombre** toohello nombre de su elemento de Marketplace. Cambiar **publisher** tooyour nombre u organización.
9. En **artefactos**, cambiar **nombre** y **ruta de acceso** toohello información correcta para la plantilla de Azure Resource Manager Hola incluidas.
   
         "artifacts": [
            {
                "name": "Type your template name",
                "type": "Template",
                "path": "DeploymentTemplates\\Type your path",
                "isDefault": true
            }
10. Reemplace **Mis elementos de Marketplace** con una lista de categorías de Hola donde debe aparecer el elemento de Marketplace.
    
             "categories":[
                 "My Marketplace Items"
              ],
11. Para las demás ediciones toomanifest.json, consulte demasiado[referencia: Marketplace elemento manifest.json](#reference-marketplace-item-manifestjson).
12. carpetas de hello toopackage en un archivo .azpkg, abra un símbolo del sistema y ejecute el siguiente comando de hello:
    
        AzureGalleryPackager.exe package –m <path toomanifest.json> -o <output location for hello package>
    
    > [!NOTE]
    > paquete de salida de toohello de ruta de acceso completa de Hello debe existir. Por ejemplo, si la ruta de acceso de salida de hello es C:\MarketPlaceItem\yourpackage.azpkg, Hola carpeta C:\MarketPlaceItem debe existir.
    > 
    > 

## <a name="publish-a-marketplace-item"></a>Publicación de un elemento de Marketplace
1. Utilice tooupload PowerShell o en el Explorador de almacenamiento de Azure su tooAzure de elemento (.azpkg) de Marketplace almacenamiento de blobs. Puede cargar el almacenamiento de Azure pila toolocal o cargue tooAzure almacenamiento. (Es una ubicación temporal para el paquete de hello). Asegúrese de que ese blob hello es accesible públicamente.
2. En hello la máquina virtual de cliente en el entorno de Microsoft Azure pila hello, asegúrese de que la sesión de PowerShell se ha configurado con sus credenciales de administrador de servicio. Encontrará instrucciones sobre cómo tooauthenticate PowerShell en la pila de Azure en [implementar una plantilla con PowerShell](azure-stack-deploy-template-powershell.md).
3. Hola de uso **AzureRMGalleryItem agregar** PowerShell cmdlet toopublish Hola Marketplace elemento tooAzure pila. Por ejemplo:
   
       Add-AzureRMGalleryItem -GalleryItemUri `
       https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   
   | Parámetro | Descripción |
   | --- | --- |
   | SubscriptionID |Identificador de suscripción de administrador de Azure. Puede recuperarlo mediante el uso de PowerShell. Si prefiere tooget en el portal de hello, vaya la suscripción del proveedor de toohello y copie Hola Id. de suscripción. |
   | GalleryItemUri |URI del BLOB para el paquete de la galería que ya se ha cargado toostorage. |
   | ApiVersion |Establecido como **2015-04-01**. |
4. Vaya toohello portal. Ahora puede ver elementos de Marketplace de hello en el portal de hello--como administrador o como un inquilino.
   
   > [!NOTE]
   > paquete de Hello podría tardar varios tooappear minutos.
   > 
   > 
5. El elemento de Marketplace ahora se ha guardado toohello Azure Marketplace de pila. Puede elegir toodelete desde la ubicación de almacenamiento de blobs.
6. Puede quitar un elemento de Marketplace mediante hello **Remove-AzureRMGalleryItem** cmdlet. Ejemplo:
   
        Remove-AzureRMGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   
   > [!NOTE]
   > Hola Marketplace de interfaz de usuario puede mostrar un error después de quitar un elemento. error de hello toofix, haga clic en **configuración** en el portal de Hola. A continuación, seleccione **Descartar modificaciones** en **Personalización del portal**.
   > 
   > 

## <a name="reference-marketplace-item-manifestjson"></a>Referencia: manifest.json del elemento de Marketplace
### <a name="identity-information"></a>Información de identidad
| Nombre | Obligatorio | Tipo | Restricciones | Descripción |
| --- | --- | --- | --- | --- |
| Nombre |X |String |[A-Za-z0-9]+ | |
| Publicador |X |String |[A-Za-z0-9]+ | |
| Versión |X |String |[SemVer v2](http://semver.org/) | |

### <a name="metadata"></a>Metadatos
| Nombre | Obligatorio | Tipo | Restricciones | Descripción |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |Se recomiendan 80 caracteres |portal de Hello podría no mostrar el nombre de elemento correctamente si tiene más de 80 caracteres. |
| PublisherDisplayName |X |String |Se recomiendan 30 caracteres |portal de Hello podría no mostrar el nombre del publicador correctamente si tiene más de 30 caracteres. |
| PublisherLegalName |X |String |256 caracteres como máximo | |
| Resumen |X |String |60 caracteres too100 | |
| LongSummary |X |String |140 caracteres too256 |Aún no se aplica a Azure Stack. |
| Descripción |X |[HTML](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |too5 500, 000 caracteres | |

### <a name="images"></a>Imágenes
Hola Marketplace utiliza Hola siguientes iconos:

| Nombre | Ancho | Alto | Notas |
| --- | --- | --- | --- |
| Ancho |255 px |115 px |Siempre se requiere |
| Grande |115 px |115 px |Siempre se requiere |
| Mediano |90 px |90 px |Siempre se requiere |
| Pequeña |40 px |40 px |Siempre se requiere |
| Instantánea |533 px |32 px |Opcional |

### <a name="categories"></a>Categorías
Cada elemento de Marketplace se debe etiquetar con una categoría que identifica de dónde aparece el elemento hello en el portal de hello interfaz de usuario. Puede elegir una de las categorías existentes de hello en la pila de Azure (proceso, datos y almacenamiento, etc.) o elija uno nuevo.

### <a name="links"></a>Vínculos
Cada elemento de catálogo de soluciones puede incluir diverso contenido tooadditional de vínculos. vínculos de Hola se especifican como una lista de nombres e identificadores URI.

| Nombre | Obligatorio | Tipo | Restricciones | Descripción |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |64 caracteres como máximo | |
| Identificador URI |X |URI | | |

### <a name="additional-properties"></a>Propiedades adicionales
En suma toohello anterior metadatos, los autores de Marketplace pueden proporcionar datos de par clave/valor personalizado en hello siguiendo el formato:

| Nombre | Obligatorio | Tipo | Restricciones | Descripción |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |25 caracteres como máximo | |
| Valor |X |String |30 caracteres como máximo | |

### <a name="html-sanitization"></a>Comprobación del estado de HTML
Para cualquier campo que permite a HTML, hello atributos y los elementos siguientes se permiten:

h1, h2, h3, h4, h5, p, ol, ul, li, a[target|href], br, strong, em, b, i

## <a name="reference-marketplace-item-ui"></a>Referencia: UI del elemento de Marketplace
Los iconos y texto para los elementos de Marketplace, tal como se muestra en el portal de Azure pila Hola son los siguientes.

### <a name="create-blade"></a>Hoja Creación
![Hoja Creación](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a>Hoja de detalles de elemento de Marketplace
![Hoja de detalles de elemento de Marketplace](media/azure-stack-marketplace-item-ui-reference/image3.png)

