---
title: "Aprovisionamiento de un conjunto de usuarios incorrecto en una aplicación de la galería de Azure AD | Microsoft Docs"
description: "Obtenga información para averiguar por qué se está aprovisionando un conjunto de usuarios para una aplicación diferente del esperado."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a>Aprovisionamiento de un conjunto de usuarios incorrecto en una aplicación de la galería de Azure AD

La selección de los usuarios que se aprovisionan para la aplicación se basa principalmente en los usuarios y los grupos que se han **asignado** a la aplicación.

Use los siguientes recursos para obtener información sobre cómo comprobar qué usuarios y grupos se han asignado a una aplicación en Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Asignación de un usuario directamente como administrador

Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:

1.  Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.

2.  Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.

3.  Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.

4.  Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.

5.  Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.

  * Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**

6.  Seleccione la aplicación que desea asignar a un usuario de la lista.

7.  Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.

8.  Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.

9.  Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.

10. Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.

11. Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**. Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.

12. **Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.

13. Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.

14. **Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.

15. Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.

Si el aprovisionamiento está configurado y ya se está ejecutando para una aplicación, los nuevos usuarios deben aprovisionarse en una aplicación en aproximadamente 10 minutos. Compruebe los **registros de auditoría** para obtener más información.

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a>Asignación de un grupo directamente a una aplicación como administrador

Para asignar uno o varios grupos a una aplicación directamente, siga los pasos siguientes:

1.  Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.

2.  Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.

3.  Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.

4.  Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.

5.  Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.

  * Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**

6.  Seleccione la aplicación que desea asignar a un usuario de la lista.

7.  Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.

8.  Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.

9.  Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.

10. Escriba el **nombre completo** del grupo al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.

11. Mantenga el puntero sobre el **grupo** en la lista para que aparezca una **casilla**. Haga clic en la casilla situada junto a la foto o el logotipo del perfil del grupo para agregar ese usuario a la lista de **seleccionados**.

12. **Opcional**: si desea **agregar más de un grupo**, escriba otro **nombre de grupo completo** o en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese grupo a la lista de **seleccionados**.

13. Cuando haya terminado de seleccionar grupos, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.

14. **Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los grupos que ha seleccionado.

15. Haga clic en el botón **Asignar** para asignar la aplicación a los grupos seleccionados.

Si el aprovisionamiento está configurado y ya se está ejecutando para una aplicación, los nuevos usuarios contenidos en el grupo deben aprovisionarse en una aplicación en aproximadamente 10 minutos. Compruebe los **registros de auditoría** para obtener más información.

>[!IMPORTANT]
>Aprovisionamiento del nombre del grupo y los detalles del grupo, además de los miembros, si se admite para algunas aplicaciones. Puede habilitar o deshabilitar esta funcionalidad habilitando o deshabilitando la **Asignación** para los objetos de grupo que se muestran en la pestaña **Aprovisionamiento**. 
>
>

Si están habilitados los grupos de aprovisionamiento, asegúrese de revisar las asignaciones de atributos para asegurarse de que se utiliza un campo apropiado para el "identificador coincidente". Esto puede ser el nombre para mostrar o el alias de correo electrónico, ya que el grupo y sus miembros no se han aprovisionado si la propiedad coincidente está vacía o no se rellenado para un grupo en Azure AD.

## <a name="next-steps"></a>Pasos siguientes
[Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md)
