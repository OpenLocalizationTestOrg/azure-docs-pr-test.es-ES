---
title: "aaaTranslate vínculos y Proxy de aplicación de las direcciones URL Azure AD | Documentos de Microsoft"
description: "Abarca conceptos básicos de hello acerca de los conectores de Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Redirección de los vínculos codificados de manera rígida para las aplicaciones publicadas con el Proxy de aplicación de Azure AD

El Proxy de aplicación de Azure AD hace su toousers disponibles de aplicaciones locales que son remotos o en sus propios dispositivos. Sin embargo, algunas aplicaciones se desarrollaron con vínculos locales incrustados en hello HTML. Estos vínculos no funcionan correctamente cuando se utiliza la aplicación hello de forma remota. Cuando haya varios local las aplicaciones punto tooeach otros, los usuarios esperan Hola vínculos tookeep trabajar cuando no están en la oficina de Hola. 

toomake de manera mejor de Hello garantiza que los vínculos funcionen Hola igual tanto dentro y fuera de la red corporativa tooconfigure Hola direcciones URL externas de su toobe de aplicaciones de la misma Hola como su direcciones URL internas. Use [dominios personalizados](active-directory-application-proxy-custom-domains.md) tooconfigure su toohave direcciones URL externa su dominio corporativo nombre en lugar de dominio de proxy de aplicación Hola predeterminado.

Si no se puede usar dominios personalizados en el inquilino, la característica de traducción de vínculo de hello del Proxy de aplicación mantiene sus vínculos trabajar independientemente de dónde están los usuarios. Si tiene aplicaciones que apuntan directamente toointernal extremos o puertos, puede asignar estas toohello las direcciones URL internas publicado direcciones URL externas Proxy de aplicación. Cuando se habilita la traducción de vínculos y el Proxy de aplicación busca a través de etiquetas de JavaScript selectas, CSS y HTML para vínculos internos publicados. A continuación, servicio de Proxy de aplicación Hola traduce para que los usuarios obtienen una experiencia sin interrupciones.

>[!NOTE]
>Hola característica de traducción de vínculo es para los inquilinos que, por cualquier motivo, no se pueden usar dominios personalizados toohave Hola mismas direcciones URL internas y externas para sus aplicaciones. Antes de habilitar esta característica, vea si los [dominios personalizados en el Proxy de aplicación de Azure AD](active-directory-application-proxy-custom-domains.md) son adecuados para usted.
>
>O bien, si aplicación hello necesita tooconfigure con traducción de vínculos de SharePoint, vea [configurar asignaciones de acceso alternativas para SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) para vínculos de toomapping de otro enfoque.

## <a name="how-link-translation-works"></a>Funcionamiento de la traducción de vínculos

Después de la autenticación, al servidor de proxy de hello pasa usuario de toohello de datos de aplicación Hola, Proxy de aplicación examina la aplicación hello para vínculos codificado de forma rígida y los reemplaza con sus respectivas publicado direcciones URL externas.

El Proxy de aplicación da por supuesto que las aplicaciones están codificadas en UTF-8. Si no es el caso de hello, especificar tipo de codificación de hello en un encabezado de respuesta http, como `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>¿Qué vínculos se ven afectados?

función de traducción de vínculos de Hello solo busca vínculos que están en las etiquetas de código en el cuerpo de Hola de una aplicación. El Proxy de aplicación tiene una característica independiente para traducir cookies o direcciones URL en los encabezados. 

Hay dos tipos comunes de vínculos internos en aplicaciones locales:

- **Los vínculos internos relativos** tooa de ese punto comparten recursos en una estructura de archivo local como `/claims/claims.html`. Estos vínculos automáticamente funcionan en aplicaciones que se publican a través de Proxy de aplicación y seguir toowork con o sin la traducción de vínculos. 
- **Los vínculos internos codificado de forma rígida** tooother aplicaciones como local `http://expenses` o publicar archivos como `http://expenses/logo.jpg`. función de traducción de vínculos de Hola funciona en los vínculos internos codificado de forma rígida y cambios de toopoint toohello direcciones URL externas que los usuarios remotos deben toogo a través de.

### <a name="how-do-apps-link-tooeach-other"></a>¿Cómo vincular tooeach otra aplicaciones?

Traducción de vínculos está habilitada para cada aplicación, para que tenga control sobre la experiencia del usuario de hello en hello por aplicación. Activar la traducción de vínculos para una aplicación cuando desee que los vínculos de hello *de* toobe de esa aplicación traducida, no los vínculos *a* esa aplicación. 

Por ejemplo, suponga que tiene tres aplicaciones publicadas a través de Proxy de aplicación que todos vinculan tooeach otro: ventajas y gastos, desplazamiento. Existe una cuarta aplicación, Comentarios, que no se publica mediante el Proxy de aplicación.

Al habilitar la traducción de vínculos para la aplicación de beneficios de hello, Hola vínculos tooExpenses y desplazamiento son las direcciones URL externas toohello redirigida para esas aplicaciones, pero no se redirige Hola vínculo tooFeedback porque no hay ninguna dirección URL externa. Vínculos de gastos y viajes tooBenefits Atrás no funcionan, porque no se habilitó la traducción de vínculos para esas dos aplicaciones.

![Vínculos desde aplicaciones de tooother ventajas cuando se habilita la traducción de vínculos](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>¿Qué vínculos no se traducen?

tooimprove rendimiento y seguridad, algunos vínculos no traducido:

- Los vínculos que no están dentro de las etiquetas de código. 
- Los vínculos que no están en HTML, CSS o JavaScript. 
- Los vínculos internos que se abren desde otros programas. No se traducirán los vínculos que se envían a través de correos electrónicos o mensajes instantáneos o que se incluyen en otros documentos. los usuarios de Hello necesitan tooknow toogo toohello dirección URL externa.

Si necesita toosupport uno de estos dos casos, use Hola mismo direcciones URL internas y externas en lugar de traducción de vínculos.  

## <a name="enable-link-translation"></a>Habilitación de la traducción de vínculos

Comenzar a trabajar con la traducción de vínculos es tan fácil como hacer clic en un botón:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Vaya demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones** > aplicación Hola seleccione desea toomanage > **Proxy de aplicación**.
3. Activar **traducir las direcciones URL en el cuerpo de la aplicación** demasiado**Sí**.

   ![Seleccione Sí tootranslate URL en el cuerpo de la aplicación](./media/application-proxy-link-translation/select_yes.png).
4. Seleccione **guardar** tooapply los cambios.

Ahora, cuando los usuarios tienen acceso a esta aplicación, proxy Hola examinará automáticamente para las direcciones URL internas que se han publicado a través de Proxy de aplicación en su inquilino.

## <a name="send-feedback"></a>Envío de comentarios

Queremos su toomake ayuda esta característica funcione para todas las aplicaciones. Se buscar más de 30 etiquetas en HTML y CSS y considere qué toosupport de casos de JavaScript. Si tiene un ejemplo de vínculos generados que no se está traduciendo, envíe un fragmento de código demasiado[comentarios de Proxy de aplicación](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Pasos siguientes
[Usar dominios personalizados con el Proxy de aplicación de Azure AD](active-directory-application-proxy-custom-domains.md) toohave Hola la misma dirección URL interna y externa

[Configurar las asignaciones alternativas de acceso en SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx)
