---
title: aaaManaging Azure recursos con el Explorador de la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse toobrowse de explorador en la nube y administrar recursos de Azure en Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Administrar los recursos de hello asociados con sus cuentas de Azure en el Explorador de Visual Studio en la nube
Explorador de nube permite tooview los recursos de Azure y grupos de recursos, inspeccionar sus propiedades y realizar acciones de diagnóstico para desarrolladores clave desde dentro de Visual Studio. 

Al igual que hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), el explorador en la nube se basa en la pila de hello Azure Resource Manager. Por lo tanto, Cloud Explorer entiende de recursos como, grupos de recursos de Azure, y de servicios de Azure, como aplicaciones lógicas y aplicaciones de API. Además, admite [control de acceso basado en rol](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Requisitos previos
- [Visual Studio de 2017](https://www.visualstudio.com/downloads/) con hello **cargas de trabajo de Azure** seleccionado, o una versión anterior de Visual Studio con hello [Microsoft Azure SDK para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Cuenta de Microsoft Azure: si todavía no tiene ninguna cuenta, puede [registrarse para una evaluación gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) o [activar las ventajas de suscriptor de Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> tooview el explorador en la nube, seleccione **vista** > **Explorer nube** en la barra de menús de Hola.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Agregar un explorador tooCloud de cuenta de Azure
recursos de hello tooview asociados con una cuenta de Azure, primero debe agregar cuenta de hello tooCloud explorador. 

1. En **Cloud Explorer**, seleccione **Configuración de la cuenta de Azure**.

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Seleccione **Agregar nueva cuenta**. 

    ![Vínculo para agregar cuenta en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Inicie sesión en la cuenta de Azure cuyos recursos desea toohello toobrowse. 

1. Una vez iniciada la sesión tooan cuenta de Azure, se muestran las suscripciones de hello asociadas con esa cuenta. Seleccione Hola casillas de verificación de las suscripciones de cuenta de hello que desee toobrowse y, a continuación, seleccione **aplicar**. 
 
    ![Explorador de nube: seleccione toodisplay de las suscripciones de Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Después de seleccionar las suscripciones de hello cuyos recursos desea toobrowse, las suscripciones y los recursos se muestran en hello explorador en la nube.

    ![Listado de recursos de Cloud Explorer para una cuenta de Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Eliminación de una cuenta de Azure de Cloud Explorer 

1. En **Cloud Explorer**, seleccione **Configuración de la cuenta de Azure**.

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Seleccione la siguiente cuenta de toohello desea tooremove, **quitar**.

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Vista de tipos de recursos o grupos de recursos
tooview los recursos de Azure, puede elegir cualquiera **tipos de recursos** o **grupos de recursos** vista.

1. En **nube explorador**, seleccione Hola lista desplegable de vista de recursos.

    ![Lista desplegable lista tooselect Hola deseado recursos del explorador de la nube](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. En menú contextual de hello, seleccione Vista de hello deseado: 

    - **Tipos de recursos** vista - Hola común usado en hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), muestra los recursos de Azure que se clasifican por su tipo, como las aplicaciones web, las cuentas de almacenamiento y máquinas virtuales. 
    - **Grupos de recursos** ver - los recursos de Azure clasifica por grupo de recursos de Azure Hola con el que está asociados. Un grupo de recursos es una agrupación de recursos de Azure, normalmente usados por una aplicación específica. toolearn más información acerca de los grupos de recursos de Azure, consulte [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).

    Hello siguiente imagen muestra una comparación de hello dos vistas de recursos:

    ![Comparación de las vistas de recursos de Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Visualización y navegación por los recursos en Cloud Explorer
toonavigate tooan recursos de Azure y ver su información en el Explorador de la nube, expanda el tipo del elemento de Hola o el grupo de recursos asociados y, a continuación, seleccione el recurso de Hola. Cuando seleccione un recurso, información aparece en las pestañas de hello dos - **acciones** y **propiedades** : en la parte inferior de hello del explorador de la nube. 

- **Acciones** pestaña - acciones de Hola de listas que puede realizar en el explorador en la nube para el recurso de hello seleccionado. También puede ver estas opciones con el botón secundario Hola recursos tooview su menú contextual.

- **Propiedades** ficha - Propiedades de Hola de muestra del recurso de hello, como su tipo, configuración regional, grupo de recursos al que está asociado.

Hello siguiente imagen muestra una comparación de ejemplo de lo que ve en cada pestaña para un servicio de aplicaciones:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Cada recurso tiene la acción de hello **abrir en el portal**. Si elige esta acción, el Explorador de nube muestra recursos Hola seleccionado en hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Hola **abrir en el portal** característica resulta práctica para navegar por los recursos de toodeeply anidado.

Acciones adicionales y los valores de propiedad también pueden aparecer en función de hello recursos de Azure. Por ejemplo, las aplicaciones web y aplicaciones lógicas también tienen acciones de hello **abrir en el explorador** y **adjuntar depurador** además demasiado**abrir en el portal**. Editores de tooopen acciones aparecen cuando se elige un blob de la cuenta de almacenamiento, una cola o una tabla. Las aplicaciones de Azure tienen las propiedades **URL** y **Status**, mientras que los recursos de almacenamiento tienen propiedades de cadena de conexión y de clave.

## <a name="find-resources-in-cloud-explorer"></a>Búsqueda de recursos en Cloud Explorer
recursos de toolocate con un nombre específico en las suscripciones de cuenta de Azure, escriba el nombre de Hola Hola **búsqueda** cuadro en el explorador en la nube.

![Buscar recursos en Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Cuando se escriben caracteres en hello **búsqueda** cuadro, solo los recursos que coinciden con los caracteres aparecen en el árbol de recursos de Hola.
