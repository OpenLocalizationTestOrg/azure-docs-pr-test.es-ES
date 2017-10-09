---
title: aaaShare Azure paneles del portal mediante el uso de RBAC | Documentos de Microsoft
description: "Este artículo explica cómo tooshare un panel en Hola portal de Azure mediante el Control de acceso basado en roles."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Uso compartido de paneles de Azure mediante el control de acceso basado en rol
Después de configurar un panel, puede publicarlo y compartirlo con otros usuarios de su organización. Permitir que otras personas tooview panel mediante Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md). Asignar un usuario o grupo de función de usuario tooa y ese rol define si los usuarios pueden ver o modificar panel publicado Hola. 

Todos los paneles publicados se implementan como recursos de Azure, lo que significa que existen como elementos administrables dentro de su suscripción y se encuentran en un grupo de recursos.  Desde una perspectiva de control de acceso, los paneles no son distintos de otros recursos como una máquina virtual o una cuenta de almacenamiento.

> [!TIP]
> Iconos individuales en el panel de Hola aplican sus propios requisitos de control de acceso basadas en los recursos de Hola que mostrar.  Por lo tanto, puede diseñar un panel que se comparte ampliamente mientras todavía proteger los datos de hello en mosaicos individuales.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Descripción del control de acceso para los paneles
Con el Control de acceso basado en roles (RBAC) puede asignar usuarios tooroles en tres niveles diferentes de ámbito:

* suscripción
* resource group
* resource

suscripción de recursos de toohello se heredan los permisos de Hola que asigna. Hola publicado panel es un recurso. Por lo tanto, quizás ya tenga tooroles de los usuarios asignados para la suscripción de Hola que también funcionan con panel publicado Hola. 

Aquí tiene un ejemplo.  Supongamos que tiene una suscripción de Azure y tienen varios miembros del equipo se han asignado los roles de Hola de **propietario**, **colaborador**, o **lector** para la suscripción de Hola. Los usuarios que son propietarios o colaboradores son pueda toolist, ver, crear, modificar o eliminar paneles dentro de suscripción de Hola.  Los usuarios que son los lectores son capaz de toolist y ver los paneles, pero no pueden modificar ni eliminarlos.  Los usuarios con acceso de lectura son toomake capaz de ediciones locales tooa publicado panel (como por ejemplo, para solucionar un problema), pero es toopublish no se puede el servidor de back-toohello de esos cambios.  Tendrán Hola opción toomake una copia privada del panel de Hola por sí mismos

Sin embargo, también puede asignar el grupo de recursos de toohello de permisos que contiene varios paneles o panel individuales tooan. Por ejemplo, puede decidir que un grupo de usuarios debe tener permisos limitados a través de la suscripción de hello pero mayor panel específico tooa de acceso. Asignar los roles de tooa a los usuarios para ese panel. 

## <a name="publish-dashboard"></a>Publicación del panel
Supongamos que ha terminado de configurar un panel que desee tooshare con un grupo de usuarios en su suscripción. pasos de Hello siguientes representan un grupo personalizado denominado Administradores de almacenamiento, pero puede nombre del grupo de lo que desea. Para obtener información sobre cómo crear un grupo de Active Directory y agregar grupo de usuarios toothat, consulte [administrar grupos en Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. En el panel de hello, seleccione **recurso compartido**.
   
     ![seleccionar recurso compartido](./media/azure-portal-dashboard-share-access/select-share.png)
2. Antes de asignar el acceso, debe publicar panel Hola. De forma predeterminada, el panel de hello estará publicado tooa grupo de recursos denominado **paneles**. Seleccione **Publicar**.
   
     ![Publicar](./media/azure-portal-dashboard-share-access/publish.png)

Tras esto, el panel ya se ha publicado. Si Hola hereden los permisos de suscripción de hello son adecuados, no es necesario toodo nada más. Otros usuarios de su organización se ser capaz de tooaccess y modificar panel Hola según su rol de nivel de suscripción. Sin embargo, para este tutorial, vamos a asignar a un grupo de función de usuario tooa para ese panel.

## <a name="assign-access-tooa-dashboard"></a>Asignar acceso tooa panel
1. Después de publicar el panel de hello, seleccione **administrar usuarios**.
   
     ![administrar usuarios](./media/azure-portal-dashboard-share-access/manage-users.png)
2. Verá una lista de los usuarios existentes que ya están asignados a un rol para este panel. La lista de usuarios existentes será diferente de la imagen de hello siguiente. Probablemente, las asignaciones de Hola se heredan de suscripción de Hola. tooadd un nuevo usuario o grupo, seleccione **agregar**.
   
     ![agregar usuario](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Seleccione el rol de Hola que representa los permisos de hello le gustaría toogrant. En este ejemplo, seleccione **Colaborador**.
   
     ![seleccionar rol](./media/azure-portal-dashboard-share-access/select-role.png)
4. Seleccione el usuario de Hola o grupo que desea tooassign toohello rol. Si no ve el usuario de Hola o grupo que está buscando en la lista de hello, use el cuadro de búsqueda de Hola. La lista de grupos disponibles dependerán de los grupos de Hola que ha creado en Active Directory.
   
     ![seleccionar usuario](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Cuando haya terminado de agregar usuarios o grupos, seleccione **Aceptar**. 
6. nueva asignación de Hola se agrega toohello lista de usuarios. Observe que su **acceso** aparece como **Asignado**, en lugar de **Heredado**.
   
     ![roles asignados](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una lista de roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).
* toolearn sobre la administración de recursos, consulte [recursos de Azure administrar a través del portal de](resource-group-portal.md).

