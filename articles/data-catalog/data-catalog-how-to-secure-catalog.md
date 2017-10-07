---
title: "aaaHow toosecure acceso tooAzure el catálogo de datos | Documentos de Microsoft"
description: "En este artículo se explica cómo toosecure el catálogo de datos y sus activos de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Cómo toosecure tener acceso a los activos de datos y catálogo toodata
> [!IMPORTANT]
> Esta característica solo está disponible en edición standard de Hola de catálogo de datos de Azure.

Catálogo de datos de Azure permite toospecify quién puede acceder al catálogo de datos de Hola y qué operaciones (registrar, anotar, tomar posesión) pueden realizar en los metadatos de catálogo de Hola. 

## <a name="catalog-users-and-permissions"></a>Usuarios del catálogo y permisos
toogive un usuario o un hello grupo acceder tooa el catálogo de datos y establecer permisos:

1. En hello [página principal de su catálogo de datos](http://www.azuredatacatalog.com), haga clic en **configuración** en la barra de herramientas de Hola.

    ![catálogo de datos: configuración](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. En la página de configuración de hello, expanda hello **usuarios catálogo** sección.
    ![Usuarios del catálogo: agregar](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Haga clic en **Agregar**.
4. Escriba Hola completo **nombre de usuario** o nombre de hello **grupo de seguridad** en hello Azure Active Directory (AAD) asociados con el catálogo de Hola. Use la coma (`,’) como separador si está agregando más de un usuario o grupo.
    ![Usuarios del catálogo: usuarios o grupos](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Presione **ENTRAR** o **ficha** fuera del cuadro de texto de Hola. 
6.  Confirme que todos los permisos (**anotar**, **registrar**, y **Take Ownership**) se asignan toothese usuarios o grupos de forma predeterminada. Es decir, Hola usuario o grupo puede [registrar activos de datos]( data-catalog-how-to-register.md), [anotar los activos de datos]( data-catalog-how-to-annotate.md), y [tomar posesión de activos de datos]( data-catalog-how-to-manage.md). 
    ![Usuarios del catálogo: permisos predeterminados](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive un usuario o grupo sólo Hola lee catálogo toohello de acceso, desactive hello **anotar** opción para ese usuario o grupo. Al hacerlo, Hola usuario o grupo no puede anotar los activos de datos en el catálogo de hello pero puede verlos. 
8.  toodeny un usuario o grupo de registro de recursos de datos, desactive hello **registrar** opción para ese usuario o grupo.
9.  un usuario tomar posesión de un recurso de datos, desactive hello toodeny **tomar posesión** opción para ese usuario o grupo. 
10. Haga clic en un usuario o grupo de usuarios del catálogo, toodelete **x** Hola/grupo de usuarios en parte inferior de Hola de lista de Hola. 
    ![Usuarios del catálogo: eliminar usuario](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > Se recomienda que agregue directamente los usuarios toocatalog de grupos de seguridad en lugar de agregar usuarios y asignar permisos. A continuación, agregar grupos de seguridad de toohello de los usuarios que coinciden con sus roles y sus catálogos de toohello de acceso necesario.

## <a name="special-considerations"></a>Consideraciones especiales

- permisos de Hello asignan toosecurity grupos son aditivas. Por ejemplo, un usuario pertenece a dos grupos. En un grupo tiene permisos de anotación y en otro no. Por lo tanto, el usuario tiene permisos de anotación. 
- asignar permisos de Hello explícitamente Hola de reemplazo de usuario de tooa permisos asignados toogroups toowhich Hola usuario pertenece. En el ejemplo anterior de hello, por ejemplo, ha agregado explícitamente usuarios de toocatalog de usuario de hello y no asigna permisos de anotar. usuario Hello no puede anotar los activos de datos aunque el usuario de hello es agregar anotaciones a un miembro de un grupo que tenga permisos.

## <a name="next-steps"></a>Pasos siguientes
- [Introducción al Catálogo de datos de Azure](data-catalog-get-started.md)

