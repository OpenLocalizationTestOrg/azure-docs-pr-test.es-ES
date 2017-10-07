---
title: "dominios de aaaCustom en el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Administrar dominios personalizados en el Proxy de aplicación de Azure AD para esa dirección URL de hello para la aplicación hello Hola igual independientemente de donde los usuarios obtener acceso a él."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Uso de dominios personalizados en el proxy de la aplicación de Azure AD

Al publicar una aplicación a través de Proxy de aplicación de Azure Active Directory, cree una dirección URL externa para su toowhen de toogo de usuarios está trabajando de forma remota. Esta dirección URL Obtiene el dominio predeterminado de hello *yourtenant.msappproxy.net*. Por ejemplo, si opta por publicar una aplicación denominada gastos y el inquilino se denomina Contoso, a continuación, dirección URL externa de hello sería https://expenses-contoso.msappproxy.net. Si desea toouse su propio nombre de dominio, configure un dominio personalizado para su aplicación. 

Se recomienda que configure dominios personalizados para las aplicaciones siempre que sea posible. Algunas de las ventajas de Hola de dominios personalizados son:

- Los usuarios pueden acceder toohello aplicación Hola la misma dirección URL, si están trabajando dentro o fuera de la red.
- Si todas las aplicaciones se hello mismas direcciones URL internas y externas, vínculos en una aplicación que señalan tooanother continuar toowork incluso fuera de la red corporativa de Hola. 
- Para controlar su marca y crear direcciones URL de Hola que desee. 


## <a name="configure-a-custom-domain"></a>Configuración de un dominio personalizado

### <a name="prerequisites"></a>Requisitos previos

Antes de configurar un dominio personalizado, asegúrese de que dispone de hello según los requisitos preparados: 
- A [tooAzure Active Directory de agregado de dominio comprobado](active-directory-domains-add-azure-portal.md).
- Un certificado personalizado para dominio hello, en forma de Hola de un archivo PFX. 
- Una aplicación local [publicada a través del proxy de la aplicación](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Configuración de un dominio personalizado

Cuando haya que esos tres requisitos listo, siga estas tooset pasos su dominio personalizado:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Navegue demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones** y elija aplicación hello desea toomanage.
3. Seleccione **Proxy de la aplicación**. 
4. En el campo de dirección URL externa de hello, utilice tooselect de lista desplegable de hello su dominio personalizado. Si no ve su dominio en la lista de hello, a continuación, que no haya comprobado todavía. 
5. Seleccione **Guardar**.
5. Hola **certificado** se habilita el campo que se ha deshabilitado. Seleccione este campo. 

   ![Haga clic en tooupload un certificado](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Si ha cargado un certificado para este dominio, el campo de certificado hello muestra información del certificado de Hola. 

6. Cargar certificados PFX de Hola y escriba la contraseña de hello para el certificado de Hola. 
7. Seleccione **guardar** toosave los cambios. 
8. Agregar un [registro DNS](../dns/dns-operations-recordsets-portal.md) que redirige Hola nuevo dominio externo de msappproxy.net de toohello de dirección URL. 

>[!TIP] 
>Solo necesita un certificado de tooupload por dominio personalizado. Una vez que cargue un certificado, puede elegir el dominio personalizado de hello al publicar una aplicación nueva y no tiene una configuración adicional toodo excepto para el registro DNS de Hola. 

## <a name="manage-certificates"></a>Administración de certificados

### <a name="certificate-format"></a>Formato del certificado
No hay ninguna restricción sobre métodos de firma de certificado de Hola. Se admiten todos los tipos de certificado habituales como, por ejemplo, la criptografía de curva elíptica (ECC) y el nombre alternativo del firmante (SAN). 

Puede usar un certificado comodín como comodín Hola coincide con la dirección URL externa de hello deseado. 

También puede usar certificados autofirmados. Si está utilizando una entidad de certificación privada, hello CDP (punto de distribución de punto de revocación de certificados) para el certificado de hello debe ser público.

### <a name="changing-hello-domain"></a>Cambiar dominio Hola
Todos los dominios comprobados aparecen en la lista de desplegable de dirección URL externa de hello para la aplicación. dominio de hello toochange, simplemente actualizar este campo para la aplicación hello. Si dominio Hola desea no está en la lista de hello, [agregarlo como un dominio comprobado](active-directory-domains-add-azure-portal.md). Si selecciona un dominio que aún no tiene un certificado asociado, siga el certificado de hello tooadd pasos 5 a 7. A continuación, asegúrese de que actualizar tooredirect de registro de DNS de Hola de dirección URL externa nueva Hola. 

### <a name="certificate-management"></a>Administración de certificados
Puede usar el mismo certificado para varias aplicaciones a menos que las aplicaciones de hello compartir un host externo de Hola. 

Obtendrá una advertencia cuando un certificado expira, indicando tooupload otro certificado a través del portal de Hola. Si se revoca el certificado de hello, los usuarios pueden ver una advertencia de seguridad al obtener acceso a la aplicación hello. No se realizan comprobaciones de revocación de los certificados.  certificado de Hola de tooupdate para una determinada aplicación, navegar por la aplicación toohello y siga los pasos 5 a 7 para configurar dominios personalizados en tooupload un nuevo certificado de las aplicaciones publicadas. Si no se utiliza los certificados antiguos de Hola por otras aplicaciones, se elimina automáticamente. 

Actualmente toda la administración de certificados es a través de páginas de aplicación individuales por lo que necesita certificados toomanage en contexto de Hola de aplicaciones relevantes de Hola. 

## <a name="next-steps"></a>Pasos siguientes
* [Habilitar inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md) tooyour publicar aplicaciones con autenticación de Azure AD.
* [Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md) tooyour las aplicaciones publicadas.
* [Agregue su tooAzure de nombre de dominio personalizado AD](active-directory-domains-add-azure-portal.md)


