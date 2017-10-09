---
title: aaaAdd un tooAzure de dominio personalizado AD | Documentos de Microsoft
description: "Explica cómo tooadd un dominio personalizado en Azure Active Directory."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Inicio rápido: Agregar un tooAzure de nombre de dominio personalizado Active Directory

Cada directorio de Azure AD viene con un nombre de dominio inicial en forma de Hola de *domainname*. onmicrosoft.com. nombre de dominio inicial de hello no se modificará ni eliminará, pero puede agregar su dominio corporativo nombre tooAzure AD así. Por ejemplo, su organización probablemente tiene otras empresas de toodo de nombres que se usan de dominio y los usuarios que inicie sesión con su nombre de dominio corporativo. Agregar nombres de dominio personalizado tooAzure AD permite tooassign nombres de usuario en el directorio de Hola que son usuarios de tooyour familiarizado, como 'alice@contoso.com.' en lugar de "alice@*<domain name>*.onmicrosoft.com". proceso de Hello es simple:

1. Agregar directorio de tooyour de nombre de dominio personalizado de Hola
2. Agregar una entrada DNS para el nombre de dominio de hello en el registrador de nombres de dominio de Hola
3. Compruebe el nombre de dominio personalizado de hello en Azure AD

## <a name="add-your-custom-domain"></a>Incorporación del dominio personalizado
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **Azure Active Directory** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.
   
   ![Apertura de Administración de usuarios](./media/active-directory-domains-add-azure-portal/user-management.png)
3. En hello ***nombre de directorio*** hoja, seleccione **nombres de dominio**.
4. En hello  ***nombre de directorio* -nombres de dominio** hoja, seleccione hello **agregar** comando.
   
   ![Al seleccionar el comando Add Hola](./media/active-directory-domains-add-azure-portal/add-command.png)
5. En hello **nombre de dominio** hoja, escriba el nombre de Hola de su dominio personalizado en el cuadro de hello, por ejemplo, "contoso.com" y, a continuación, seleccione **Agregar dominio**. Ser seguro tooinclude Hola .com, .net u otra extensión de nivel superior.
6. En hello ***nombre de dominio*** hoja (con el nombre de dominio personalizado en el título de hello), obtener información de entrada DNS toouse tooverify que su organización es propietaria de nombre de dominio personalizado de Hola Hola.
   
   ![Obtención de información de entrada de DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Si tiene previsto toofederate local Windows Server AD con Azure AD, deberá hello tooselect **tengo intención de tooconfigure este dominio para el inicio de sesión único con mi servicio Active Directory local** casilla cuando se ejecuta la herramienta de hello Azure AD Connect toosynchronize los directorios. También necesita tooregister Hola el mismo nombre de dominio que seleccionó para la federación con su directorio local en hello **dominio de Azure AD** paso a paso en el Asistente de Hola. Puede ver qué paso en el Asistente de hello parece que [en estas instrucciones](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Si no tiene la herramienta de hello Azure AD Connect, puede [descargarlo aquí](http://go.microsoft.com/fwlink/?LinkId=615771).

Ahora que ha agregado el nombre de dominio de hello, Azure AD debe comprobar que su organización es propietaria de nombre de dominio de Hola. Antes de Azure AD puede llevar a cabo esta comprobación, debe agregar una entrada DNS en el archivo de zona DNS de Hola Hola nombre de dominio. Esta tarea se realiza en el sitio Web de hello para el registrador de nombres de dominio para el nombre de dominio de Hola.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Agregar entrada DNS de hello en hello registrador de nombres de dominio de Hola
Hola siguiente paso toouse el nombre de su dominio personalizado con Azure AD es tooupdate el archivo de zona DNS de hello para el dominio de Hola. Azure AD, a continuación, puede comprobar que su organización es propietaria de nombre de dominio personalizado de Hola.

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
4. En hello ***nombre de dominio*** hoja (es decir, Hola hoja que se abre con el nuevo nombre de dominio en el título de hello), seleccione **compruebe** comprobación de hello toocomplete.

> [!TIP]
> Puede agregar nombres de dominio personalizado de too900, pero sólo uno puede ser [establecer como nombre de dominio principal de Hola para su directorio Azure AD](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) utiliza de forma predeterminada al crear nuevas cuentas.

Ahora puede crear cuentas de usuario basadas en la nube, o actualizar información de cuentas de usuario locales sincronizadas previamente, con el nombre de dominio personalizado. También puede modificar usuario sincronizado anteriormente cuenta dominio sufijo información mediante [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Solución de problemas
Si no se puede comprobar un nombre de dominio personalizado, pruebe Hola siguiendo los pasos de solución de problemas:

1. **Espere una hora**. Los registros DNS deben toopropagate antes de Azure AD puede comprobar el dominio de Hola. Esto puede tardar una hora o más.
2. **Asegúrese de Hola se escribió el registro de DNS y que es correcta**. Complete este paso en el sitio Web de hello para el registrador de nombres de dominio de hello para el dominio de Hola. Azure AD no puede comprobar el nombre de dominio de hello si Hola entrada DNS no está presente en hello archivo de zona DNS o si no es una coincidencia exacta con la entrada DNS de Hola que Azure AD proporcionado. Si no tiene registros DNS de acceso tooupdate de dominio de hello en el registrador de nombres de dominio de hello, compartir la entrada DNS de hello con hello persona o equipo de la organización que tiene este acceso y pídale entrada DNS de tooadd Hola.
3. **Eliminar el nombre de dominio de Hola de otro directorio de Azure AD**. Se puede comprobar el nombre de dominio en solo un único directorio. Si previamente se ha comprobado un nombre de dominio en otro directorio, se debe eliminar allí antes de que se puede comprobar en el nuevo directorio. leer toolearn acerca de cómo eliminar los nombres de dominio, [administrar nombres de dominio personalizados](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Incorporación de más nombres de dominio personalizados
Si su organización usa más de un nombre de dominio personalizado, como 'contoso.com' y 'contosobank.com', puede agregar más seguridad too900 repitiendo los pasos de hello en este artículo para cada uno.

### <a name="learn-more"></a>Más información
[Información general conceptual de los nombres de dominio personalizados en Azure Active Directory](active-directory-add-domain-concepts.md)

[Managing custom domain names (Administración de nombres de dominio).](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo tooadd una tooAzure de dominio personalizado AD. 

Puede usar Hola siguiendo el vínculo tooadd un nuevo dominio personalizado en Azure AD de hello portal de Azure.

> [!div class="nextstepaction"]
> [Agregar un dominio personalizado](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 