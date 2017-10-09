---
title: aaaAdd nuevos usuarios tooAzure Active Directory | Documentos de Microsoft
description: "Explica cómo tooadd nuevos usuarios en Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Inicio rápido: Agregar nuevos usuarios tooAzure Active Directory
Este artículo explica cómo tooadd nuevos usuarios de su organización en Azure Active Directory (Azure AD) Hola uno a la vez mediante el portal de Azure de Hola o mediante la sincronización, el usuario de Windows Server AD local datos de la cuenta. 

## <a name="add-cloud-based-users"></a>Adición de usuarios basados en la nube
1. Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **Azure Active Directory** y, después, **Usuarios y grupos**.
3. En hello **usuarios y grupos** hoja, seleccione **todos los usuarios**y, a continuación, seleccione **nuevo usuario**.
   ![Al seleccionar el comando Add Hola](./media/add-users-azure-active-directory/add-user.png)
4. Escriba los detalles de usuario de hello, como **nombre** y **nombre de usuario**. Hello parte del nombre de dominio del nombre de usuario de hello debe estar Hola predeterminado inicial dominio nombre ".onmicrosoft.com [nombre de dominio]" o comprobado, no federadas [nombre de dominio personalizado](add-custom-domain.md) como "contoso.com".
5. Copia o en caso contrario hello de nota contraseña generada por el usuario para que puede proporcionarlo toohello usuario una vez completado este proceso.
6. Si lo desea, puede abrir y rellene la información de Hola Hola **perfil** hoja, hello **grupos** hoja o hello **rol del directorio** hoja para el usuario de Hola. Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).
7. En hello **usuario** hoja, seleccione **crear**.
8. Distribuir segura Hola genera contraseña toohello nuevo usuario, para que hello usuario puede iniciar sesión en.

> [!TIP]
> También puede sincronizar datos de las cuentas de usuario desde una instancia local de Windows Server AD. Soluciones de identidad de Microsoft abarcan local y capacidades en la nube, crear una identidad de usuario único para la autenticación y autorización de recursos de tooall, independientemente de su ubicación. A esto le llamamos identidad híbrida. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) puede ser usado toointegrate sus directorios locales con Azure Active Directory para los escenarios de identidad híbrida. Esto le permite tooprovide una identidad común para los usuarios para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Eliminación de usuarios desde Azure AD
1. Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **Usuarios y grupos**.
3. En hello **usuarios y grupos** hoja, seleccione Hola usuario toodelete de lista de Hola. 
4. En la hoja de hello para el usuario seleccionado de hello, seleccione **Introducción**y, a continuación, en la barra de comandos de hello, seleccione **eliminar**.
   ![Al seleccionar el comando Add Hola](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Más información 
* [Agregar un usuario externo](active-directory-users-create-external-azure-portal.md)

* [Asignar un rol de usuario tooa en Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo tooadd nuevos usuarios tooAzure AD Premium. 

Puede usar Hola siguiendo el vínculo toocreate un nuevo usuario en Azure AD de hello portal de Azure.

> [!div class="nextstepaction"]
> [Agregar usuarios tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
