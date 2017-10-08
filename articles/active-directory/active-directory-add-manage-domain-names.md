---
title: nombres de dominio personalizado de aaaManaging en Azure Active Directory | Documentos de Microsoft
description: "Conceptos y procedimientos de administración de un dominio personalizado en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Administración de los nombres de dominio personalizados en Azure Active Directory
Un nombre de dominio puede ser un identificador importante para muchos recursos de directorio, como parte de:

* Un nombre de usuario o una dirección de correo electrónico de un usuario
* dirección de Hola para un grupo
* URI del Id. de aplicación de Hello para una aplicación

Un recurso en Azure Active Directory (Azure AD) puede incluir un nombre de dominio que ya se comprobó toobe propiedad de directorio de Hola que contiene recursos de Hola. Solo los administradores globales pueden realizar tareas de administración de Azure AD.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo toomanage los nombres de dominio en el centro de administración de hello Azure AD, consulte [administrar nombres de dominio personalizado en Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Establecer el nombre de dominio principal de Hola para su directorio Azure AD
Cuando se crea el directorio, el nombre de dominio inicial de hello, por ejemplo, "contoso.onmicrosoft.com", también es nombre de dominio principal de hello para el directorio. dominio principal de Hello es el nombre de dominio de predeterminado de Hola para un nuevo usuario cuando se crea un nuevo usuario en hello [portal de Azure clásico](https://manage.windowsazure.com/), otros portales como portal de administración de Office 365 Hola o. Esto simplifica el proceso de Hola para un administrador toocreate nuevos usuarios portal Hola.

nombre de dominio principal de toochange hello para el directorio:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con una cuenta de usuario que sea un administrador global de su directorio Azure AD.
2. Seleccione **Active Directory** en la barra de navegación izquierda de Hola.
3. Abra el directorio.
4. Seleccione hello **dominios** ficha.
5. Seleccione hello **cambio principal** botón de barra de comandos de Hola.
6. Seleccione dominio Hola que quiere toobe Hola nueva principal del dominio de su directorio.

Puede cambiar el nombre de dominio principal de hello para el directorio toobe cualquier dominio personalizado comprobado que no es federada. Cambiar dominio principal de hello para el directorio no cambiará los nombres de usuario de Hola para todos los usuarios existentes.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Agregar nombres de dominio personalizado tooyour Azure AD
Puede sumar el directorio de Azure AD de tooeach de nombres de dominio personalizado de too900. Hola proceso demasiado[agregar un nombre de dominio personalizados adicionales](active-directory-add-domain.md) Hola mismo para el primer nombre de dominio personalizado Hola.

## <a name="add-subdomains-of-a-custom-domain"></a>Adición de subdominios de un dominio personalizado
Si desea que tooadd un nombre de dominio de tercer nivel, como 'europe.contoso.com' tooyour directory, primero debe agregar y comprobar el dominio de segundo nivel de hello, por ejemplo, contoso.com. subdominio Hola se comprobarán automáticamente por Azure AD. se ha comprobado toosee que Hola subdominio que acaba de agregar, página de actualización de hello en el Explorador de Hola que enumera los dominios de hello en el directorio.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>¿Qué toodo si cambia el registrador de DNS de hello para el nombre de dominio personalizado
Si cambia el registrador de DNS de hello para el nombre de dominio personalizado, puede continuar toouse nombre de dominio personalizado con Azure AD sin interrupción y sin tareas de configuración adicionales. Si usa el nombre de dominio personalizado con Office 365, Intune u otros servicios que se basan en nombres de dominio personalizado en Azure AD, consulte la documentación de toohello para esos servicios.

## <a name="delete-a-custom-domain-name"></a>Eliminación de un nombre de dominio personalizado
Puede eliminar un nombre de dominio personalizado de Azure AD si su organización ya no utiliza ese nombre de dominio, o si necesita toouse ese nombre de dominio con otro Azure AD.

toodelete un nombre de dominio personalizado, primero debe asegurarse de que no hay recursos en el directorio se basan en nombre de dominio de Hola. No puede eliminar un nombre de dominio de su directorio si:

* Cualquier usuario tiene un nombre de usuario, la dirección de correo electrónico o la dirección de proxy que incluyen el nombre de dominio de Hola.
* Cualquier grupo tiene una dirección de correo electrónico o la dirección de proxy que incluye el nombre de dominio de Hola.
* Cualquier aplicación en Azure AD tiene una identificador URI que incluye el nombre de dominio de Hola de aplicación.

Debe cambiar o eliminar dichos recursos en su directorio Azure AD antes de poder eliminar el nombre de dominio personalizado de Hola.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Usar nombres de dominio toomanage PowerShell o API Graph
También se pueden completar la mayoría de las tareas de administración para los nombres de dominio de Azure Active Directory mediante Microsoft PowerShell, o mediante programación utilizando la API de Azure Graph.

* [Usar nombres de dominio de toomanage de PowerShell de Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Usar nombres de dominio de toomanage de API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Pasos siguientes
* [Obtenga más información acerca de los nombres de dominio en Azure AD](active-directory-add-domain-concepts.md)
* [Managing custom domain names (Administración de nombres de dominio).](active-directory-add-manage-domain-names.md)

