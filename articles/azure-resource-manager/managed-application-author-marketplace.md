---
title: aaaAzure administra las aplicaciones de hello Marketplace | Documentos de Microsoft
description: "Azure se describen las aplicaciones que están disponibles a través de hello Marketplace administrado."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Las aplicaciones de Hola Marketplace administrado de Azure

 Pueden usar varios MSP, ISV e integradores de sistema (SIs) Azure administra aplicaciones toooffer sus clientes de Azure Marketplace de soluciones tooall. Estas soluciones reducen mantenimiento hello y sobrecarga de mantenimiento para los clientes. Pueden vender publicadores de infraestructura y el software a través de hello Marketplace. Pueden adjuntar soporte operacional toomanaged aplicaciones y servicios. Para más información, consulte [Información general sobre las aplicaciones administradas](managed-application-overview.md).

Este artículo explica cómo un MSP, ISV o SI puede publicar un toohello aplicación Marketplace y hacer que toocustomers ampliamente disponibles.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Requisitos previos para publicar una aplicación administrada

Requisitos previos toolisting Hola Marketplace:

* Requisitos previos técnicos

    *  Para obtener información acerca de la estructura básica de Hola y la sintaxis de plantillas del Administrador de recursos de Azure, consulte [plantillas de Azure Resource Manager](resource-group-authoring-templates.md).
    *  soluciones de tooview plantilla completa, consulte [plantillas de inicio rápido de Azure](https://azure.microsoft.com/en-us/documentation/templates/) o hello [repositorio de plantilla de inicio rápido](https://github.com/azure/azure-quickstart-templates).
    *  Para obtener información acerca de cómo toocreate Hola interfaz para los clientes que implementación la aplicación a través de hello Marketplace, vea [crear un archivo de definición de interfaz de usuario](managed-application-createuidefinition-overview.md).

* Requisitos previos no técnicos (empresariales)

    *   Su empresa o sus filiales deben encontrarse en un país o región donde se admiten las ventas por hello Marketplace.
    *   Debe tener una licencia del producto de forma que sea compatible con facturación modelos admitidos por hello Marketplace.
    *   Es responsabilidad suya toocustomers de soporte técnico disponibles de manera comercialmente razonable. compatibilidad de Hello puede ser libre, de pago, o a través de la Comunidad de soporte.
    *   Asimismo, es responsable de la concesión de licencias para su software y las dependencias de software de terceros.
    *   Debe proporcionar el contenido que cumpla los criterios de la oferta toobe enumerados en el Marketplace de Hola y Hola portal de Azure.
    *   Debe aceptar toohello términos del acuerdo de publicador y directivas de participación de hello Azure Marketplace.
    *   Debe aceptar toocomply con hello las condiciones de uso, la declaración de privacidad de Microsoft y contrato de programa de certificación de Microsoft Azure.

## <a name="create-a-new-azure-application-offer"></a>Creación de una nueva oferta de aplicación de Azure

Después de cumplir los requisitos previos de hello, está listo toocreate su oferta de la aplicación administrada. Hagamos un repaso rápido a los conceptos de oferta y de SKU.

### <a name="offer"></a>Oferta

oferta de Hola para una aplicación administrada corresponde tooa clase de producto de la oferta de un publicador. Si tiene un nuevo tipo de solución o aplicación que desea toomake disponible en hello Marketplace, se puede configurar como una oferta nueva. Una oferta es una colección de SKU. Cada oferta aparece como su propia entidad Hola Marketplace.

### <a name="sku"></a>SKU

Un SKU es Hola unidad más pequeña puede adquirir de una oferta. Puede usar una SKU de hello mismo producto (oferta) de la clase toodifferentiate entre:

* Distintas características que se admiten.
* Si la oferta de hello es managed o unmanaged.
* Los modelos de facturación que se admiten.

Una SKU aparece debajo de la oferta de primario Hola Hola Marketplace. Aparece como su propia entidad puede adquirir en hello portal de Azure.

### <a name="set-up-an-offer"></a>Configuración de una oferta

1. Inicie sesión en toohello [portal de partners de nube](https://cloudpartner.azure.com/).

2. En el panel de navegación de Hola Hola izquierda, seleccione **+ oferta nueva** > **aplicaciones de Azure**.

    ![Nueva oferta](./media/managed-application-author-marketplace/newOffer.png)

3. Rellenar formularios de Hola que aparecen en hello restante en hello **Editor** vista. Los campos obligatorios están marcados con un asterisco rojo (*).

    ![Configuración de oferta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Cuatro formas básicas son toocreate usa una aplicación administrada:

    a. Configuración de oferta

    b. SKU

    c. Marketplace

    d. Soporte técnico

Estos formatos se describen con más detalle en las secciones siguientes de Hola.

## <a name="offer-settings-form"></a>Formulario de configuración de oferta
Use esta configuración de oferta de forma básica toospecify Hola.

1. Rellene hello **ofrecen configuración** formulario. Hola distintos campos son:

    a. **Identificador de la oferta**: este identificador único identifica Hola oferta dentro de un perfil de publicador. Este identificador se muestra en las direcciones URL de producto, las plantillas de Resource Manager y los informes de facturación. Puede contener solo caracteres alfanuméricos en minúscula o guiones (-). Id. de Hello no puede terminar con un guión. Es limitado tooa máximo de 50 caracteres. En cuanto se lanza una oferta, este campo se bloquea.

    b. **Id. de publicador**: usar este perfil de publicador de lista desplegable toochoose Hola desea toopublish esta oferta en. En cuanto se lanza una oferta, este campo se bloquea.

    c. **Nombre**: este nombre para mostrar para su oferta aparece en hello Marketplace y en el portal de Hola. Puede tener un máximo de 50 caracteres. Incluya un nombre de marca que identifique el producto. No incluya aquí el nombre de su empresa a menos que sea así como se comercializa. Si está marketing esta oferta en su propio sitio Web, asegúrese de que ese nombre hello es exactamente cómo aparece en el sitio Web.

2. Seleccione **guardar** toosave su progreso. 

## <a name="skus-form"></a>Formulario de SKU
Hola siguiente paso es tooadd SKU para su oferta.

1. Seleccione **SKU** > **SKU nueva**. 

    ![Selección de SKU nueva](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Escriba un **Identificador de SKU**. Un identificador de SKU es un identificador único para hello SKU dentro de una oferta. Este identificador se muestra en las direcciones URL de producto, las plantillas de Resource Manager y los informes de facturación. Puede contener solo caracteres alfanuméricos en minúscula o guiones (-). Id. de Hello no puede terminar con un guión y es limitado tooa máximo de 50 caracteres. En cuanto se lanza una oferta, este campo se bloquea. Puede tener varias SKU dentro de una oferta. Necesita una SKU para cada imagen piensa toopublish.

3. Rellene hello **detalles del SKU** sección en hello siguiendo el formato:

    ![Proporcionar una nueva SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Rellene Hola siguientes campos:
    
    a. **Título**: escriba un título para esta SKU. Este título aparece en la Galería de Hola para este elemento.

    b. **Resumen**: proporcione un breve resumen de esta SKU. Este texto aparece debajo del título de Hola.

    c. **Descripción**: escriba una descripción detallada acerca de hello SKU.

    d. **Tipo de SKU**: Hola valores permitidos son **aplicación administrada** y **plantillas de solución**. En este caso, seleccione **Aplicación administrada**.

4. Rellene hello **detalles del paquete** sección en hello siguiendo el formato:

    ![Paquete](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Rellene Hola siguientes campos:

    a. **Versión actual**: escriba una versión de paquete de hello cargar. Debe estar en formato de hello `{number}.{number}.{number}{number}`.

    b. **Seleccione un archivo de paquete**: este paquete contiene los siguientes archivos que se comprimen en un archivo .zip de hello:
    * **applianceMainTemplate.json**: archivo de plantilla de implementación de Hola que ha usado toodeploy Hola/aplicación de la solución. Para obtener información acerca de cómo ver archivos de plantilla de implementación de toocreate, [crear la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: interfaz de usuario de Hola de toogenerate portal Azure de Hola que ha usado tooprovision esta solución/aplicación usa este archivo. Para más información, consulte [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: este archivo de plantilla contiene solo los recursos de Microsoft.Solution/appliances de Hola. archivo de Hello mainTemplate incluye Hola propiedades siguientes:

        *  **tipo**: Use **Marketplace** para las aplicaciones administradas en hello Marketplace.
        *  **ManagedResourceGroupId**: este grupo de recursos de suscripción del cliente de hello es donde se implementan todos los recursos de hello definidos en applianceMainTemplate.json.
        *  **PublisherPackageId**: esta cadena identifica de forma única los paquetes de saludo. Proporcionan un valor con formato Hola Hola `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Obtener hello **identificador ofrecen** y **Id. de publicador** de hello publicación portal, como se muestra en hello después de imagen:

![Id. de oferta](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Obtener hello **identificador de SKU**, tal y como se muestra en hello después de imagen:

![Identificador de SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Obtener paquete hello **versión**, tal y como se muestra en hello después de imagen:

![Versión del paquete](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  En función de hello anteriores ejemplos, Hola valor de **PublisherPackageId** es `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Ejemplo de mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Este paquete debe contener el resto de las plantillas anidada o scripts que son necesario toosuccessfully aprovisionar esta aplicación. Hello mainTemplate.json, applianceMainTemplate.json y applianceCreateUIDefinition.json archivos deben estar presentes en la carpeta raíz de Hola.

* **Autorizaciones**: esta propiedad define quién obtiene hello y acceso de nivel de acceso de recursos de toohello en las suscripciones de los clientes. publicador de Hello utilizarla toomanage aplicación de hello en nombre de cliente de Hola.
* **PrincipalId**: esta propiedad es el identificador de hello Azure Active Directory (Azure AD) de un usuario, el grupo de usuarios o la aplicación que ha concedido ciertos permisos en recursos de Hola de suscripción del cliente de Hola. Hola definición de rol describe los permisos de Hola. 
* **Definición de roles**: esta propiedad es una lista de todos los Hola Control de acceso basado en roles (RBAC) roles integrados proporcionados por Azure AD. Puede seleccionar Hola rol de recursos de Hola de toomanage toouse más apropiados en nombre del cliente de Hola.

Puede agregar varias autorizaciones. Se recomienda que cree un grupo de usuarios de AD y especifique su identificador en **PrincipalId**. De esta manera, puede agregar el grupo de usuarios de toohello a los usuarios más sin necesidad de Hola tooupdate Hola SKU.

Para obtener más información sobre la RBAC, consulte [comience a usar RBAC en hello portal de Azure](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Formulario de Marketplace

Hola formulario Marketplace solicita campos que se muestran en hello [Azure Marketplace](https://azuremarketplace.microsoft.com) y en hello [portal de Azure](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>Id. de suscripción de versión preliminar

Escriba una lista de identificadores que puede tener acceso a la oferta de hello después de haberlo publicado de suscripción de Azure. Puede usar estos oferta de hello muestra una vista previa de lista blanca suscripciones tootest antes de efectuarlo live. Puede compilar una lista blanca de configurar las suscripciones de too100 en el portal de partners de Hola.

### <a name="suggested-categories"></a>Categorías sugeridas

Seleccione las categorías de toofive de lista de Hola que su oferta puede estar asociada mejor. Estas categorías es toomap usado en las categorías de producto de oferta toohello que están disponibles en hello [Azure Marketplace](https://azuremarketplace.microsoft.com) hello y [portal de Azure](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

Resumen de Hola de las aplicaciones administradas muestra hello siguientes campos:

![Resumen de Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

Hola **Introducción** ficha correspondiente a la aplicación administrada muestra hello siguientes campos:

![Introducción a Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

Hola **planes + precios** ficha correspondiente a la aplicación administrada muestra hello siguientes campos:

![Planes de Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Azure Portal

Resumen de Hola de las aplicaciones administradas muestra hello siguientes campos:

![Resumen del portal](./media/managed-application-author-marketplace/publishvm12.png)

información general de Hola para una aplicación administrada muestra hello siguientes campos:

![Información general de Azure Portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Directrices para logotipos

Siga estas directrices para ningún logotipo que se carga en el portal de partners de la nube de hello:

*   Hola diseño de Azure tiene una paleta de colores simple. Limitar el número de Hola de principal y los colores de base de datos secundaria en el logotipo.
*   colores del tema Hola de portal de hello son blancos y negros. No use estos colores como color de fondo de hello para el logotipo. Usar un color que realiza su logotipo destacada en el portal de Hola. Nosotros recomendamos usar colores primarios simples. *Si usa un fondo transparente, asegúrese de que Hola logotipo y texto no están blancos, negro o azul.*
*   No use un fondo degradado en logotipo Hola.
*   No coloque el texto en el logotipo de hello, ni siquiera su empresa o nombre de la marca. Hola apariencia y funcionamiento de su logotipo debe ser sin formato y evite degradados.
*   Asegúrese de que no ajusta el logotipo de Hola.

#### <a name="hero-logo"></a>Logotipo de imagen prominente

logotipo de héroe de Hello es opcional. publicador de Hello puede elegir no tooupload un logotipo héroe. Después de carga el icono de héroe de hello, no se puede eliminar. En ese momento, socio Hola debe seguir instrucciones de Marketplace de Hola para iconos héroe.

Siga estas directrices para el icono del logotipo de hello héroe:

*   nombre para mostrar Hello publicador, título de plan de Hola y oferta de hello resumida largas se muestran en blanco. Por lo tanto, no use un color claro para el fondo de hello del icono de héroe de Hola. Los fondos transparentes y de color negro o blanco no pueden utilizarse en los iconos de imagen prominente.
*   Después de que se muestra la oferta de hello, publicador Hola nombre para mostrar, título del plan de hello, resumidas largas de oferta de Hola y Hola **crear** botón incrustados mediante programación dentro de logotipo héroe de Hola. Por lo tanto, no se especifica ningún texto mientras diseña el logotipo de héroe de Hola. Dejar espacios en blanco en hello derecho porque texto hello se incluye mediante programación en ese espacio. espacio vacío de Hola para texto hello debe ser 415 x 100 píxeles en hello derecho. Se ve compensado por 370 píxeles de hello izquierda.

    ![Ejemplo de logotipo de imagen prominente](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Formulario de soporte técnico

Rellene hello **admite** formulario con el soporte técnico se pone en contacto de su empresa. Esta información podría contener contactos de ingeniería y contactos de soporte técnico al cliente.

## <a name="publish-an-offer"></a>Publicación de una oferta

Después de rellenar todas las secciones de hello, seleccione **publicar** proceso de hello toostart que hace que su toocustomers disponible de la oferta.

## <a name="next-steps"></a>Pasos siguientes

* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada](managed-application-overview.md).
* Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).
* Para información sobre cómo publicar una aplicación administrada del catálogo de servicios, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).
* Para información sobre cómo usar una aplicación administrada del catálogo de servicios, consulte [Uso de una aplicación administrada del catálogo de servicios](managed-application-consumption.md).
