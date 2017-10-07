---
title: "recursos de red CDN de Azure de aaaSecuring con autenticación de token | Documentos de Microsoft"
description: "Usar autenticación de token toosecure acceso tooyour CDN de Azure a los activos."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Protección de los activos de la red CDN de Azure con autenticación por tokens

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Información general

Autenticación de token es un mecanismo que permite tooprevent CDN de Azure desde que sirve al activos toounauthorized clientes.  Esto se hace normalmente tooprevent "hotlinking" de contenido, que otro sitio Web, a menudo un panel de mensajes, usa los activos sin permiso.  lo que puede repercutir en los costos de la entrega de contenido. Al habilitar esta característica en la red CDN, las solicitudes se autenticarán por borde CDN POP antes de entregar contenido Hola. 

## <a name="how-it-works"></a>Cómo funciona

Autenticación de token comprueba las solicitudes son generadas por un sitio de confianza exigiendo solicitudes toocontain un valor de símbolo (token) que contiene información codificada acerca de solicitante de Hola. Contenido sólo se servirá toorequester Hola codificado en requisitos de hello cumple la información, en caso contrario, se denegarán las peticiones. Puede configurar el requisito de hello con uno o varios parámetros siguiente.

- País: permitir o denegar las solicitudes que se ha originado en determinados países.  [Lista de códigos de país válidos.](https://msdn.microsoft.com/library/mt761717.aspx) 
- Dirección URL: Permitir solo toorequest activo o ruta de acceso especificada.  
- Host: permitir o denegar solicitudes que utilizan los hosts especificados en el encabezado de solicitud de Hola.
- Origen de referencia: permitir o denegar el toorequest de origen de referencia especificado.
- Dirección IP: permitir sólo las solicitudes cuyo origen es una dirección IP específica o subred IP concretas.
- Protocolo: permitir o bloquear las solicitudes basadas en el protocolo de hello usan contenido de hello toorequest.
- Fecha de expiración: asignar una fecha y hora tooensure período que un vínculo solo es válido durante un período de tiempo limitado.

Vea el ejemplo de configuración detallada de cada parámetro.

## <a name="reference-architecture"></a>Arquitectura de referencia

Vea a continuación de una arquitectura de referencia de configuración de autenticación de token en la red CDN toowork a su aplicación Web.

![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Lógica de validación de tokens en el punto de conexión de red CDN
    
Este gráfico describe cómo Azure CDN valida la solicitud del cliente cuando se configura la autenticación por tokens en el punto de conexión de red CDN.

![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Configuración de la autenticación por tokens

1. De hello [portal de Azure](https://portal.azure.com), perfil de CDN tooyour y, a continuación, haga clic en hello **administrar** portal complementario de botón toolaunch Hola.

    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Mantenga el mouse sobre **HTTP grandes**y, a continuación, haga clic en **Auth Token** de Hola de elementos flotantes. En esta pestaña configurará la clave y los parámetros de cifrado.

    1. Escriba una clave de cifrado única para **Primary Key** (Clave principal).  Especifique otra para **Backup Key** (Clave de copia de seguridad).

        ![Clave de configuración de autenticación por tokens de la red CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Configure los parámetros de cifrado con la herramienta de cifrado (permitir o denegar las solicitudes según el tiempo de expiración, el país, el origen de referencia, el protocolo y la dirección IP del cliente. Puede usar cualquier combinación).

        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - ec_expire: asigna una fecha de expiración a un token después de un tiempo especificado. Solicitudes presentadas después de que se denegará la hora de expiración de Hola. Este parámetro utiliza la marca de tiempo de Unix (en función de los segundos transcurridos desde la época estándar de 1/1/1970 00:00:00 GMT. También puede usar herramientas en línea de conversión de tooprovide entre la hora estándar y la hora de Unix).  Por ejemplo, si desea tooset Hola token toobe expirado en 31/12/2016 12:00:00 GMT, utilice Hola Unix tiempo: 1483185600 como sigue:
    
        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - permitir que la dirección url de EC: permite activo en particular tooa tootailor símbolos (tokens) o ruta de acceso. Restringe toorequests acceso iniciar cuya dirección URL con una ruta de acceso relativa específica. Es posible incluir varias rutas de acceso si las separa con comas. Las direcciones URL distinguen mayúsculas de minúsculas. Función de requisitos de hello, puede configurar otro valor tooprovide nivel de acceso diferente. A continuación se muestran un par de escenarios:
        
            Si tiene una dirección URL: http://www.mydomain.com/pictures/city/strasbourg.png. Consulte el valor de entrada "" y el nivel de acceso correspondiente

            1. Valor de entrada "/": se permitirán todas las solicitudes
            2. Valor de entrada "/ imágenes": hello todas las siguientes solicitudes se permitirá
            
                - http://www.mydomain.com/pictures.png
                - http://www.mydomain.com/pictures/city/strasbourg.png
                - http://www.mydomain.com/picturesnew/city/strasbourgh.png
            3. Valor de entrada "/pictures/": solo se permitirán las solicitudes de /pictures/
            4. Valor de entrada "/pictures/city/strasbourg.png": solo permiten solicitudes para este activo
    
        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - ec_country_allow: solo permite solicitudes que se originen en uno o más países especificados. Se denegarán las solicitudes que se originen en los demás países. Utilice tooset de código de país los parámetros de Hola y separando cada código de país con una coma. Por ejemplo, si desea tener acceso tooallow de Estados Unidos y Francia, entrada US, FR en columna de hello como a continuación.  
        
        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - ec_country_deny: deniega solicitudes que se originen en uno o más países especificados. Se permitirán las solicitudes que se originen en los demás países. Utilice tooset de código de país los parámetros de Hola y separando cada código de país con una coma. Por ejemplo, si desea tener acceso toodeny de Estados Unidos y Francia, entrada US, FR en columna de Hola.
    
        - ec_ref_allow: solo se permiten solicitudes del origen de referencia especificado. Un origen de referencia identifica Hola URL de página web de Hola que vinculan el recurso toohello que se solicita. valor del parámetro de origen de referencia de Hello no debe incluir el protocolo de Hola. Puede escribir un nombre de host o una ruta de acceso determinada en ese nombre de host. También puede agregar varios orígenes de referencia dentro de un único parámetro si los separa con comas. Si ha especificado un valor de origen de referencia, pero no se envía información de origen de referencia de hello en solicitud de hello debido toosome configuración del explorador, estas solicitudes se denegarán de forma predeterminada. Puede asignar a "Ausente" o un valor en blanco en hello parámetro tooallow estas solicitudes con la que falta información de origen de referencia. También puede usar "*. consoto.com" tooallow todos los subdominios de consoto.com.  Por ejemplo, si desea tener acceso de tooallow para las solicitudes de www.consoto.com, todos los subdominios en consoto2.com y erquests con reffers en blanco o falta, debajo del valor de entrada:
        
        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - ec_ref_deny: deniega solicitudes del origen de referencia especificado. Consulte toodetails y ejemplo de parámetro "ec-ref-permitir".
         
        - ec_proto_allow: solo se permiten solicitudes del protocolo especificado. Por ejemplo, http o https.
        
        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - ec_proto_deny: deniega las solicitudes del protocolo especificado. Por ejemplo, http o https.
    
        - CE IPCliente: restringe la dirección IP del solicitante de acceso toospecified. Se admiten tanto IPV4 como IPV6. Puede especificar la dirección IP de solicitud única o la subred IP.
            
        ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Puede probar el token con la herramienta de descifrado de Hola.

    4. También puede personalizar el tipo de saludo de respuesta que se devolverán toouser cuando se deniega la solicitud. De forma predeterminada se usa 403.

3. Ahora haga clic en la ficha **Motor de reglas** en **HTTP Large** (HTTP grandes). Utilizará esta característica pestaña toodefine las rutas de acceso tooapply hello, habilitar la característica de autenticación de token de hello y habilitar la autenticación de token adicional relacionados con las capacidades.

    - Usar activos de "IF" columna toodefine o ruta de acceso que desea que la autenticación de token tooapply. 
    - Haga clic en tooadd "Auth símbolo (token)" de la autenticación de token de hello característica desplegable tooenable.
        
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. Hola **motor de reglas** ficha, hay algunas funciones adicionales que puede habilitar.
    
    - Símbolo (token) de código de autorización de denegación: determina el tipo de saludo de respuesta que se devolverán toouser cuando se deniegue una solicitud. Las reglas que configure aquí sobrescribirá la configuración de código de denegación de hello en la pestaña de la autenticación de token de Hola.
    - Omitir la autenticación de token: determina si el token de dirección URL que usan toovalidate serán entre mayúsculas y minúsculas.
    - Parámetro de token de autenticación: cambiar el nombre de consulta de autenticación de token de hello parámetro de cadena que muestra de Hola la dirección URL solicitada. 
        
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Puede personalizar el token, que es una aplicación que genera el token para las características de autenticación basadas en tokens. Se puede acceder al código fuente aquí en [GitHub](https://github.com/VerizonDigital/ectoken).
Idiomas disponibles:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Precios de las características y los proveedores de Azure CDN

Vea hello [información general de la red CDN](cdn-overview.md) tema.
