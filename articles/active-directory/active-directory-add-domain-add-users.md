---
title: usuarios aaaAssign tooa dominio personalizado en Azure Active Directory | Documentos de Microsoft
description: "¿Cómo toopopulate un dominio personalizado en Azure Active Directory con cuentas de usuario."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Asignar los usuarios de dominio personalizado de tooa
Después de haber agregado su tooAzure Active Directory de dominio personalizado, debe agregar cuentas de usuario de Hola para este dominio para que pueda empezar a autenticarlos.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo toomanage los nombres de dominio en el centro de administración de hello Azure AD, consulte [administrar nombres de dominio personalizado en Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Usuarios sincronizados desde un directorio local
Si ya se han configurado una conexión entre sus instalaciones en Active Directory y Azure Active Directory, la sincronización puede rellenar las cuentas de Hola. Para obtener más información sobre cómo toosynchronize Azure Active Directory con su Active Directory local, vea [integrar las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Usuarios agregan y administran en la nube de Hola
dominio de hello toochange para una cuenta de usuario existente:

1. Abra hello Azure portal clásico con una cuenta que sea un administrador global o un administrador del usuario.
2. Abra el directorio.
3. Seleccione hello **usuarios** ficha.
4. Seleccione usuario Hola de hello lista.
5. Cambiar el dominio de hello para el usuario de hello y, a continuación, seleccione **guardar**.

Esto también puede hacerse mediante [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Selección de un dominio personalizado al crear un nuevo usuario
1. Abra hello Azure portal clásico con una cuenta que sea un administrador global o un administrador del usuario.
2. Abra el directorio.
3. Seleccione hello **usuarios** ficha.
4. En la barra de comandos de hello, seleccione **agregar**.
5. Cuando se agrega el nombre de usuario de hello, elija dominio personalizado de hello en lista de dominios de Hola.
6. Seleccione **Guardar**.

## <a name="next-steps"></a>Pasos siguientes
* [Uso de dominio personalizado nombres toosimplify Hola inicio de sesión experiencia para los usuarios](active-directory-add-domain.md)
* [Managing custom domain names (Administración de nombres de dominio).](active-directory-add-manage-domain-names.md)
* [Información general conceptual de nombres de dominio personalizado en Azure Active Directory](active-directory-add-domain-concepts.md)

