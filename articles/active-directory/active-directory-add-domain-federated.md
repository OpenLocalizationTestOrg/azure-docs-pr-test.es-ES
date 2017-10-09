---
title: "aaaAdd el nombre de dominio personalizado y establecer seguridad federada de inicio de sesión tooAzure Active Directory | Documentos de Microsoft"
description: "¿Cómo tooadd de su empresa nombres de dominio tooset de Active Directory tooAzure inicio de sesión federado en entre Azure Active Directory y la solución de federación local"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Agregue su tooAzure de nombre de dominio personalizado Active Directory
Puede configurar un nombre de dominio personalizado, como 'contoso.com', para que los usuarios de contoso.com puedan tener un inicio de sesión único federado de la red corporativa. Si ya tiene los servicios de federación de Active Directory (AD FS) o un servidor de federación diferentes que se ejecutan en su red corporativa, puede configurar Azure AD toouse nombre de dominio personalizado mediante la herramienta de Azure AD Connect Hola. También puede usar el entorno de Azure AD Connect toodeploy un nuevo AD FS y configure para federado único inicio de sesión tooAzure AD.

Si no es necesario y no piensa toodeploy AD FS u otro servidor de federación, siga estas instrucciones: [agregar un tooAzure de nombre de dominio personalizado Active Directory](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Agregar un directorio de tooyour de nombre de dominio personalizado
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con una cuenta de usuario que sea un administrador global de su directorio Azure AD.
2. En **Active Directory**, abra el directorio y seleccione hello **dominios** ficha.
3. En la barra de comandos de hello, seleccione **agregar**y, a continuación, escriba nombre de Hola de su dominio personalizado, por ejemplo, "contoso.com". Ser seguro tooinclude Hola .com, .net u otra extensión de nivel superior.
4. Seleccione hello **tengo intención de tooconfigure este dominio para el inicio de sesión único con mi servicio Active Directory local** casilla de verificación.
5. Seleccione **Agregar**.

Ejecutar hello Azure AD Connect herramienta tooget Hola DNS entrada que Azure AD utilizará tooverify Hola dominio. Verá una entrada DNS de Hola Hola **dominio de Azure AD** paso a paso en el Asistente de Hola. Puede ver qué paso en el Asistente de hello parece que [en estas instrucciones](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Si no tiene la herramienta de hello Azure AD Connect, puede [descargarlo aquí](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Agregar entrada DNS de hello en hello registrador de nombres de dominio de Hola
Hola siguiente paso toouse el nombre de su dominio personalizado con Azure AD es tooupdate el archivo de zona DNS de hello para el dominio de Hola. Esto permite tooverify de Azure AD que su organización es propietaria de nombre de dominio personalizado de Hola.

1. Inicie sesión en el sitio Web de toohello para el registrador de nombres de dominio para el nombre de dominio. Si no tienes acceso toodo esto, pida Hola persona o equipo en su organización que tenga este paso de toocomplete de acceso 2 y toolet que saber cuando se completan.
2. Actualizar archivo de zona DNS de hello para el dominio de hello agregando tooyou de hello DNS entrada proporcionada por Azure AD. Esta entrada DNS permite a Azure AD tooverify la propiedad de dominio de Hola. Hola entrada DNS no cambia los comportamientos, como el enrutamiento de correo electrónico o de hospedaje web.

Para obtener ayuda con este paso, lea [Instrucciones para agregar entradas DNS en los registradores DNS más habituales](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Compruebe el nombre de dominio de hello con Azure AD
Cuando haya agregado la entrada DNS de hello, son nombre de dominio de hello tooverify listo con Azure AD.

dominio de hello tooverify, seleccione **siguiente** en hello **dominio de Azure AD** paso del Asistente para conectar de hello Azure AD. Azure AD tendrá un aspecto para la entrada DNS de hello en el archivo de zona DNS de hello para el dominio de Hola. Azure AD solo Comprobar nombre de dominio de Hola una vez que se hayan propagado los registros DNS de Hola. La propagación suele tardar unos segundos, pero a veces puede tardar una hora o incluso más. Si la comprobación no funciona Hola primera vez, inténtelo de nuevo más tarde.

A continuación, continúe con hello restantes pasos del Asistente de Azure AD Connect de Hola. Esto hará que sincronicen los usuarios de su tooAzure de Windows Server AD AD. Los usuarios sincronizados de dominio de Hola que configuró para la federación será capaz de tooget un federado inicio de sesión único que aportan los AD tooAzure de red corporativa.

## <a name="troubleshooting"></a>Solución de problemas
Si no se puede comprobar un nombre de dominio personalizado, intente Hola siguiente. Comenzaremos con hello más comunes y de trabajo hacia abajo toohello menos comunes.

1. **Espere una hora**. Los registros DNS deben toopropagate antes de Azure AD puede comprobar el dominio de Hola. Esto puede tardar una hora o más.
2. **Asegúrese de Hola se escribió el registro de DNS y que es correcta**. Complete este paso en el sitio Web de hello para el registrador de nombres de dominio de hello para el dominio de Hola. Azure AD no puede comprobar el nombre de dominio de hello si Hola entrada DNS no está presente en hello archivo de zona DNS o si no es una coincidencia exacta con la entrada DNS de Hola que Azure AD proporcionado. Si no tiene registros DNS de acceso tooupdate de dominio de hello en el registrador de nombres de dominio de hello, compartir la entrada DNS de hello con hello persona o equipo de la organización que tiene este acceso y pídale entrada DNS de tooadd Hola.
3. **Eliminar el nombre de dominio de Hola de otro directorio de Azure AD**. Se puede comprobar el nombre de dominio en solo un único directorio. Si previamente se ha comprobado un nombre de dominio en otro directorio, se debe eliminar allí antes de que se puede comprobar en el nuevo directorio. leer toolearn acerca de cómo eliminar los nombres de dominio, [administrar nombres de dominio personalizados](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Incorporación de más nombres de dominio personalizados
Si su organización usa varios nombres de dominio personalizado, como 'contoso.com' y 'contosobank.com', se puede agregar una tooa máximo de 900 nombres de dominio. Usar hello mismo los pasos de este artículo tooadd cada de sus nombres de dominio.

## <a name="next-steps"></a>Pasos siguientes
* [Managing custom domain names (Administración de nombres de dominio).](active-directory-add-manage-domain-names.md)
* [Información general conceptual de nombres de dominio personalizado en Azure Active Directory](active-directory-add-domain-concepts.md)
* [Incorporación de la personalización de marca de empresa a sus páginas de inicio de sesión y panel de acceso](active-directory-add-company-branding.md)
* [Usar nombres de dominio de toomanage de PowerShell de Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

