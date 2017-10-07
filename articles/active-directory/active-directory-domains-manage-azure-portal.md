---
title: nombres de dominio personalizado de aaaManaging en Azure Active Directory | Documentos de Microsoft
description: "Conceptos y procedimientos de administración de un nombre de dominio en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Administración de los nombres de dominio personalizados en Azure Active Directory
Un nombre de dominio es una parte importante del identificador de Hola para muchos recursos de directorio: forma parte de una dirección de correo electrónico o nombre de usuario para un usuario, parte de la dirección de Hola para un grupo y puede formar parte del URI del Id. de aplicación de hello para una aplicación. Un recurso en Azure Active Directory (Azure AD) puede incluir un nombre de dominio que ya se ha comprobado como propiedad de directorio de Hola que contiene recursos de Hola. Solo los administradores globales pueden realizar tareas de administración de Azure AD.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Establecer el nombre de dominio principal de Hola para su directorio Azure AD
Cuando se crea el directorio, nombre de dominio inicial de hello, por ejemplo, "contoso.onmicrosoft.com", también es el nombre del dominio principal de Hola. dominio principal de Hello es nombre de dominio predeterminado de Hola para un nuevo usuario cuando se crea un nuevo usuario. Establecer un nombre de dominio principal simplifica el proceso de Hola para un administrador toocreate nuevos usuarios portal Hola. nombre de dominio principal de Hola toochange:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.
   
   ![Apertura de Administración de usuarios](./media/active-directory-domains-add-azure-portal/user-management.png)
3. En hello ***nombre de directorio*** hoja, seleccione **nombres de dominio**.
4. En hello  ***nombre de directorio* -nombres de dominio** hoja, nombre de dominio de hello select que desea que el nombre de dominio principal de toomake Hola.
5. En hello ***nombre de dominio*** hoja (es decir, Hola hoja que se abre con el nuevo nombre de dominio en el título de hello), seleccione hello **convertir en principal** comando. Confirme la elección cuando se le pregunte.
   
   ![Conversión de un nombre de dominio en principal](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Puede cambiar el nombre de dominio principal de hello para el directorio toobe cualquier dominio personalizado comprobado que no es federada. Cambiar dominio principal de hello para el directorio no cambiará los nombres de usuario de Hola para todos los usuarios existentes.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Agregar nombres de dominio personalizado tooyour Azure AD
Puede sumar el directorio de Azure AD de tooeach de nombres de dominio personalizado de too900. Hola proceso demasiado[agregar un nombre de dominio personalizados adicionales](add-custom-domain.md) Hola mismo para el primer nombre de dominio personalizado Hola.

## <a name="add-subdomains-of-a-custom-domain"></a>Adición de subdominios de un dominio personalizado
Si desea que tooadd un nombre de dominio de tercer nivel, como 'europe.contoso.com' tooyour directory, primero debe agregar y comprobar el dominio de segundo nivel de hello, por ejemplo, contoso.com. subdominio Hola se comprobarán automáticamente por Azure AD. se ha comprobado toosee que Hola subdominio que acaba de agregar, página de actualización de hello en el Explorador de Hola que enumera los dominios de Hola.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>¿Qué toodo si cambia el registrador de DNS de hello para el nombre de dominio personalizado
Si cambia el registrador de DNS de hello para el nombre de dominio personalizado, puede continuar toouse nombre de dominio personalizado con Azure AD sin interrupción y sin tareas de configuración adicionales. Si usa el nombre de dominio personalizado con Office 365, Intune u otros servicios que se basan en nombres de dominio personalizado en Azure AD, consulte la documentación de toohello para esos servicios.

## <a name="delete-a-custom-domain-name"></a>Eliminación de un nombre de dominio personalizado
Puede eliminar un nombre de dominio personalizado de Azure AD si su organización ya no utiliza ese nombre de dominio, o si necesita toouse ese nombre de dominio con otro Azure AD.

toodelete un nombre de dominio personalizado, primero debe asegurarse de que no hay recursos en el directorio se basan en nombre de dominio de Hola. No puede eliminar un nombre de dominio de su directorio si:

* Cualquier usuario tiene un nombre de usuario, la dirección de correo electrónico o la dirección de proxy que incluye el nombre de dominio de Hola.
* Cualquier grupo tiene una dirección de correo electrónico o la dirección de proxy que incluye el nombre de dominio de Hola.
* Cualquier aplicación en Azure AD tiene una identificador URI que incluye el nombre de dominio de Hola de aplicación.

Debe cambiar o eliminar dichos recursos en su directorio Azure AD antes de poder eliminar el nombre de dominio personalizado de Hola.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Usar nombres de dominio toomanage PowerShell o API Graph
También se pueden completar la mayoría de las tareas de administración para los nombres de dominio de Azure Active Directory mediante Microsoft PowerShell, o mediante programación utilizando la API de Azure Graph.

* [Usar nombres de dominio de toomanage de PowerShell de Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Usar nombres de dominio de toomanage de API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Pasos siguientes
* [Agregar nombres de dominio personalizados](add-custom-domain.md)

