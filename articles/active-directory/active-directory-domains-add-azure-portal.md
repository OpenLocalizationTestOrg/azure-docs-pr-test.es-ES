---
title: nombre de su dominio personalizado de aaaAdd tooAzure Active Directory | Documentos de Microsoft
description: "Cómo tooadd de su empresa nombres de dominio tooAzure Active Directory, y cómo tooverify Hola nombre de dominio."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Agregar un tooAzure de nombre de dominio personalizado Active Directory
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-domains-add-azure-portal.md)
> * [Portal de Azure clásico](active-directory-add-domain.md)
> 

Con Azure Active Directory (Azure AD), puede agregar su dominio corporativo nombre tooAzure AD así. Podría tener los nombres de dominio que su organización usa toodo empresa y los usuarios que inicie sesión con su nombre de dominio corporativo. Agregar tooAzure de nombre de dominio de hello AD permite nombres de usuario de tooassign en el directorio de Hola que son usuarios de tooyour familiarizado, como 'alice@contoso.com.' proceso de Hello es simple:

1. Agregar directorio de tooyour de nombre de dominio personalizado de Hola
2. Agregar una entrada DNS para el nombre de dominio de hello en el registrador de nombres de dominio de Hola
3. Compruebe el nombre de dominio personalizado de hello en Azure AD

## <a name="how-do-i-add-a-domain-name"></a>¿Cómo se agrega un nombre de dominio?
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.
   
   ![Apertura de Administración de usuarios](./media/active-directory-domains-add-azure-portal/user-management.png)
3. En hello ***nombre de directorio*** hoja, seleccione **nombres de dominio**.
4. En hello  ***nombre de directorio* -nombres de dominio** hoja, seleccione hello **agregar** comando.
   
   ![Al seleccionar el comando Add Hola](./media/active-directory-domains-add-azure-portal/add-command.png)
5. En hello **nombre de dominio** hoja, escriba el nombre de Hola de su dominio personalizado en el cuadro de hello, por ejemplo, "contoso.com" y, a continuación, seleccione **Agregar dominio**. Ser seguro tooinclude Hola .com, .net u otra extensión de nivel superior.
6. En hello ***domainname*** hoja (es decir, Hola hoja que se abre con el nuevo nombre de dominio en el título de hello), obtener información de entrada DNS de Hola que Azure AD utilizará tooverify que su organización es propietaria de nombre de dominio personalizado de Hola.
   
   ![Obtención de información de entrada de DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Ahora que ha agregado el nombre de dominio de hello, Azure AD debe comprobar que su organización es propietaria de nombre de dominio de Hola. Antes de Azure AD puede llevar a cabo esta comprobación, debe agregar una entrada DNS en el archivo de zona DNS de Hola Hola nombre de dominio. Esta tarea se realiza en el sitio Web de hello para el registrador de nombres de dominio para el nombre de dominio de Hola.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Agregar entrada DNS de hello en hello registrador de nombres de dominio de Hola
Hola siguiente paso toouse el nombre de su dominio personalizado con Azure AD es tooupdate el archivo de zona DNS de hello para el dominio de Hola. Esto permite tooverify de Azure AD que su organización es propietaria de nombre de dominio personalizado de Hola.

1. Inicie sesión en el registrador de nombres de dominio de toohello dominio Hola. Si no tienes Hola de tooupdate acceso entrada DNS, pregunte persona Hola o equipo que tenga este paso de toocomplete de acceso 2 y toolet que saber cuando se completan.
2. Actualizar archivo de zona DNS de hello para el dominio de hello agregando tooyou de hello DNS entrada proporcionada por Azure AD. Esta entrada DNS permite a Azure AD tooverify la propiedad de dominio de Hola. Hola entrada DNS no cambia los comportamientos, como el enrutamiento de correo electrónico o de hospedaje web.

Para obtener ayuda con esta entrada DNS agrega hello, lea [instrucciones para agregar una entrada DNS en registradores populares de DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Compruebe el nombre de dominio de hello con Azure AD
Cuando haya agregado la entrada DNS de hello, son nombre de dominio de hello tooverify listo con Azure AD.

Un nombre de dominio se puede comprobar solo una vez propagan los registros DNS de Hola. Esta propagación a suele tardar unos segundos, pero a veces puede tardar una hora o incluso más. Si la comprobación no funciona Hola primera vez, inténtelo de nuevo más tarde.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **examinar**, escriba administración de usuarios en el cuadro de texto de hello y, a continuación, seleccione **ENTRAR**.
   
   ![Apertura de Administración de usuarios](./media/active-directory-domains-add-azure-portal/user-management.png)
3. En hello **administración de usuarios: los nombres de dominio** hoja, nombre de dominio no comprobado de hello select que deseas tooverify.
4. En hello ***domainname*** hoja (es decir, Hola hoja que se abre con el nuevo nombre de dominio en el título de hello), seleccione **compruebe** comprobación de hello toocomplete.

Ya puede [asignar nombres de usuario que incluyan su nombre de dominio personalizado](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Solución de problemas
Si no se puede comprobar un nombre de dominio personalizado, intente Hola siguiente. Comenzaremos con hello más comunes y de trabajo hacia abajo toohello menos comunes.

1. **Espere una hora**. Los registros DNS deben toopropagate antes de Azure AD puede comprobar el dominio de Hola. Esto puede tardar una hora o más.
2. **Asegúrese de Hola se escribió el registro de DNS y que es correcta**. Complete este paso en el sitio Web de hello para el registrador de nombres de dominio de hello para el dominio de Hola. Azure AD no puede comprobar el nombre de dominio de hello si Hola entrada DNS no está presente en hello archivo de zona DNS o si no es una coincidencia exacta con la entrada DNS de Hola que Azure AD proporcionado. Si no tiene registros DNS de acceso tooupdate de dominio de hello en el registrador de nombres de dominio de hello, compartir la entrada DNS de hello con hello persona o equipo de la organización que tiene este acceso y pídale entrada DNS de tooadd Hola.
3. **Eliminar el nombre de dominio de Hola de otro directorio de Azure AD**. Se puede comprobar el nombre de dominio en solo un único directorio. Si previamente se ha comprobado un nombre de dominio en otro directorio, se debe eliminar allí antes de que se puede comprobar en el nuevo directorio. leer toolearn acerca de cómo eliminar los nombres de dominio, [administrar nombres de dominio personalizados](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Incorporación de más nombres de dominio personalizados
Si su organización usa varios nombres de dominio personalizado, como 'contoso.com' y 'contosobank.com', se puede agregar una tooa máximo de 900 nombres de dominio. Usar hello mismo los pasos de este artículo tooadd cada de sus nombres de dominio.

## <a name="next-steps"></a>Pasos siguientes
[Managing custom domain names (Administración de nombres de dominio).](active-directory-domains-manage-azure-portal.md)

