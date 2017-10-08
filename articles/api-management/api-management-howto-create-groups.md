---
title: "las cuentas de desarrollador aaaManage usar los grupos de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage developer cuentas con grupos de administración de API de Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Cómo para desarrolladores de toomanage grupos toocreate y usar las cuentas de administración de API de Azure
Administración de API, los grupos son utilizados toomanage Hola visibilidad de toodevelopers de productos. Productos son la primera toogroups visible realizadas y, a continuación, pueden ver y suscribirse toohello productos que están asociados a grupos de Hola a los desarrolladores de esos grupos. 

Administración de API tiene Hola los grupos de sistema inmutables siguientes.

* **Administradores** : los administradores de la suscripción de Azure son miembros de este grupo. Los administradores administran las instancias de servicio de administración de API, crear Hola API, operaciones y productos que se usan los programadores.
* **Desarrolladores** : los usuarios del portal para desarrolladores autenticados se incluyen en este grupo. Los desarrolladores son clientes de Hola que compilan aplicaciones mediante las API. Los programadores se conceden portal para desarrolladores de acceso toohello y creación aplicaciones que llaman a operaciones de Hola de una API.
* **Los invitados** -sin autenticar usuarios del portal para desarrolladores, como clientes potenciales visitar el portal para desarrolladores de Hola de una caída de la instancia de administración de API en este grupo. Se pueden conceder cierto acceso de solo lectura, como la capacidad de hello tooview API, pero no llamarlos.

En grupos de sistema de toothese de suma, los administradores pueden crear grupos personalizados o [aprovechar grupos externos en inquilinos de Azure Active Directory asociados][leverage external groups in associated Azure Active Directory tenants]. Grupos personalizados y externos pueden usarse junto con grupos del sistema para conceder a los desarrolladores visibilidad y tener acceso a los productos tooAPI. Por ejemplo, podría crear un grupo personalizado para desarrolladores afiliados a una determinada organización de socios y permitan tener acceso toohello las API de un producto que contiene solo las API relevantes. Un usuario puede ser miembro de más de un grupo.

En esta guía se muestra cómo los administradores de una instancia de Administración de API pueden agregar nuevos grupos y asociarlos a productos y desarrolladores.

> [!NOTE]
> Además toocreating y administrar grupos en el portal para desarrolladores de hello, puede crear y administrar grupos mediante la API de REST de administración de hello [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidad.
> 
> 

## <a name="create-group"></a>Creación de un grupo
toocreate un nuevo grupo, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API.

![Portal del publicador][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Haga clic en **grupos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **Agregar grupo**.

![Add new group][api-management-add-group]

Escriba un nombre único para el grupo de hello y una descripción opcional y haga clic en **guardar**.

![Add new group][api-management-add-group-window]

Hola nuevo grupo se mostrará en Hola de hello grupos ficha tooedit **nombre** o **descripción** del grupo de hello, haga clic en nombre de hello del grupo de hello en lista de Hola. grupo de hello toodelete, haga clic en **eliminar**.

![Group added][api-management-new-group]

Hello grupo una vez creada, se puede asociar con los productos y los desarrolladores.

## <a name="associate-group-product"></a>Asociación de un grupo a un producto
tooassociate un grupo con un producto, haga clic en **productos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en nombre de Hola de producto de su preferencia Hola.

![Set visibility][api-management-add-group-to-product]

Seleccione hello **visibilidad** ficha tooadd y quitar grupos y tooview Hola actual para el producto de Hola. tooadd o quitar grupos, active o desactive las casillas de verificación de Hola para hello deseado grupos y haga clic en **guardar**.

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> los grupos de Azure Active Directory tooadd, consulte [cómo tooauthorize developer cuentas con Azure Active Directory en la administración de API de Azure](api-management-howto-aad.md).
> 
> grupos de tooconfigure de hello **visibilidad** para un producto, haga clic en **administrar grupos**.
> 
> 

Una vez que un producto está asociado a un grupo, los desarrolladores de ese grupo pueden ver y suscribirse toohello producto.

## <a name="associate-group-developer"></a>Asociación de grupos a desarrolladores
grupos tooassociate con desarrolladores, haga clic en **usuarios** de hello **administración de API** menú Hola izquierda y, a continuación Hola casilla situada junto a los desarrolladores de hello desea tooassociate con un grupo.

![Agregar toogroup de desarrollador][api-management-add-group-to-developer]

Una vez Hola deseado se comprueban los desarrolladores, haga clic en grupo que quiera hello en hello **agregar tooGroup** lista desplegable. Los desarrolladores se pueden quitar de grupos mediante el uso de hello **quitar del grupo** lista desplegable. 

![Desarrolladores][api-management-add-group-to-developer-saved]

Una vez agregado asociación Hola entre para desarrolladores de Hola y el grupo de hello, puede verlo en hello **usuarios** ficha.

## <a name="next-steps"></a>Pasos siguientes
* Una vez que un programador se agrega grupo tooa, pueden ver y suscribirse productos toohello asociados a dicho grupo. Para obtener más información, consulte [Creación y publicación de un producto en Azure API Management][How create and publish a product in Azure API Management].
* Además toocreating y administrar grupos en el portal para desarrolladores de hello, puede crear y administrar grupos mediante la API de REST de administración de hello [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidad.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
