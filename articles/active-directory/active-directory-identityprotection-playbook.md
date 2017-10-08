---
title: "Guía de Active Directory Identity Protection aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Azure AD Identity Protection permite capacidad de hello toolimit de un tooexploit atacante una identidad en peligro o el dispositivo y toosecure una identidad o un dispositivo que era toobe sospechosa o conocido en peligro."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Guía de Azure Active Directory Identity Protection
Esta guía le ayudará a:

* Rellenar los datos en el entorno de protección de identidad de hello vulnerabilidades y simular eventos de riesgo
* Configurar directivas de acceso condicional basado en riesgo y Hola impacto de estas directivas en las pruebas

## <a name="simulating-risk-events"></a>Simulación de eventos de riesgo
En esta sección se proporciona los pasos necesarios para simular Hola siguientes tipos de eventos de riesgo:

* Inicios de sesión desde direcciones IP anónimas (fácil)
* Inicios de sesión desde ubicaciones desconocidas (moderada)
* Viaje imposible tooatypical ubicaciones (difíciles)

Otros eventos de riesgo no se pueden simular de forma segura.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Inicios de sesión desde direcciones IP anónimas
Este tipo de evento de riesgo identifica los usuarios que han iniciado sesión correctamente desde una dirección IP que se ha identificado como una dirección IP de proxy anónima. Estos servidores proxy son la utilizan los usuarios que quieran toohide dirección IP de su dispositivo y puede utilizarse de forma malintencionada.

**toosimulate en un inicio de sesión desde una IP anónima, realizar pasos de Hola**:

1. Descargar hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).
2. Utilice Hola Tor Browser, para navegar demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Escriba las credenciales de Hola de cuenta de hello que desea tooappear Hola **inicios de sesión desde direcciones IP anónimas** informes.

inicio de sesión de Hola se mostrará en el panel de la protección de la identidad de Hola intervalos de 5 minutos. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Inicios de sesión desde ubicaciones desconocidas
riesgo de ubicaciones desconocidas Hello es un mecanismo de evaluación de inicio de sesión en tiempo real que considera más allá de las ubicaciones de inicio de sesión (IP, latitud y longitud y ASN) toodetermine nuevo / familiarizado ubicaciones. sistema Hola almacena direcciones IP anterior, latitud o longitud y ASN de un usuario y tiene en cuenta estas ubicaciones familiarizado toobe. Una ubicación de inicio de sesión se considera familiarizada si hello ubicación de inicio de sesión no coincide con ninguno de ubicaciones Hola existente.

Azure Active Directory Identity Protection:  

* Tiene un período de aprendizaje inicial de 14 días, durante el cual no marca ninguna nueva ubicación como ubicación desconocida.
* omite los inicios de sesión desde dispositivos conocidos y ubicaciones geográficamente cerrar tooan existente familiarizado ubicación.

toosimulate ubicaciones desconocidas, tiene toosign en desde una ubicación y un dispositivo que cuenta hello no ha firmado en de antes. 

**toosimulate un inicio de sesión de desde una ubicación familiarizado, realizar pasos de Hola**:

1. Elija una cuenta que tenga al menos un historial de inicios de sesión de 14 días. 
2. Realice uno de estos pasos:
   
   a. Al usar una VPN, navegue demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com) y escriba Hola credenciales de cuenta de hello que desea eventos de riesgo de hello toosimulate para.
   
   b. Pide a un colaborador en un toosign de otra ubicación con credenciales de la cuenta de hello (no recomendadas).

inicio de sesión de Hola se mostrará en el panel de la protección de la identidad de Hola intervalos de 5 minutos.

### <a name="impossible-travel-tooatypical-location"></a>Viaje imposible tooatypical ubicación
Simular la condición de viaje imposible hello es difícil porque algoritmo hello usa tooweed de aprendizaje de máquina out falsos positivos como viaje imposible desde dispositivos conocidos, o inicios de sesión de VPN que se utilizan por otros usuarios en el directorio de Hola. Además, el algoritmo de Hola requiere un historial de inicio de sesión de 3 días de too14 para usuario de hello antes de comenzar la generación de eventos de riesgo.

**toosimulate una ubicación de tooatypical viaje imposible, realizar pasos de Hola**:

1. Mediante el explorador estándar, navegue demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Escriba Hola credenciales de cuenta de hello para que desea toogenerate un evento de riesgo de viaje imposible.
3. Cambie el agente de usuario. Puede cambiar el agente de usuario en Internet Explorer desde Herramientas de desarrollo, o bien en Firefox o Chrome con un complemento modificador del agente de usuario.
4. Cambie la dirección IP. Puede cambiar la dirección IP mediante una VPN, un complemento de Tor, o iniciando una máquina nueva en Azure en otro centro de datos.
5. Inicio de sesión en demasiado[https://myapps.microsoft.com](https://myapps.microsoft.com) utilizando Hola mismas credenciales como antes y dentro de unos minutos después de inicio de sesión anterior en Hola.

inicio de sesión de Hola se mostrará en el panel de protección de la identidad de hello dentro de 2 a 4 horas.<br>
Debido a la máquina complejas de hello implicados modelos de aprendizaje, es probable que no obtenga recogerán.<br> Conviene tooreplicate estos pasos para varias cuentas de Azure AD.

## <a name="simulating-vulnerabilities"></a>Simulación de puntos vulnerables
Los puntos vulnerables son puntos débiles de un entorno de Azure AD que puede ser aprovechados por un actor perjudicial. Actualmente se exponen 3 tipos de puntos vulnerables en Azure AD Identity Protection que aprovechan otras características de Azure AD. Estas vulnerabilidades se mostrará en el panel de la protección de la identidad de hello automáticamente una vez que se configuran estas características.

* Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* [Privileged Identity Management](active-directory-privileged-identity-management-configure.md)de Azure AD. 

## <a name="user-compromise-risk"></a>Riesgo de compromiso de usuario
**tootest riesgo del compromiso de usuario, realizar pasos de Hola**:

1. Inicio de sesión en demasiado[https://portal.azure.com](https://portal.azure.com) con credenciales de administrador global para el inquilino.
2. Navegue demasiado**Identity Protection**. 
3. En hello principal **Azure AD Identity Protection** hoja, haga clic en **configuración**. 
4. En hello **configuración del Portal** hoja, en **las reglas de seguridad**, haga clic en **riesgo del compromiso de usuario**. 
5. En hello **iniciar sesión en riesgo** hoja, activar **Habilitar regla** desactivada y, a continuación, haga clic en **guardar** configuración.
6. Para una cuenta de usuario determinada, simule un evento de riesgo de ubicaciones desconocidas o IP anónima. Esto elevará nivel de riesgo de usuario de Hola para ese usuario demasiado**medio**.
7. Espere unos minutos y después compruebe que el nivel de usuario para el usuario sea **Medio**.
8. Vaya toohello **configuración del Portal** hoja.
9. En hello **riesgo del compromiso de usuario** hoja, en **Habilitar regla**, seleccione **en** . 
10. Seleccione una de las siguientes opciones de hello:
    
    a. tooblock, seleccione **medio** en **bloque iniciar sesión en**.
    
    b. cambio de contraseña segura tooenforce, seleccione **medio** en **requerir la autenticación multifactor**.
11. Haga clic en **Guardar**.
12. Ahora puede probar el acceso condicional basado en riesgos mediante un inicio de sesión con un usuario con un nivel de riesgo elevado. Si el riesgo de usuario de hello es medio, dependiendo de la directiva de configuración de hello, el inicio de sesión es bloqueará cualquiera o se convierten obligatoriamente toochange su contraseña. 
    <br><br>
    ![Guía de](./media/active-directory-identityprotection-playbook/201.png "guía")
    <br>

## <a name="sign-in-risk"></a>Riesgo de inicio de sesión
**tootest un inicio de sesión en riesgo, lleve a cabo Hola pasos:**

1. Inicio de sesión en demasiado[https://portal.azure.com ](https://portal.azure.com) con credenciales de administrador global para el inquilino.
2. Navegue demasiado**Identity Protection**.
3. En hello principal **Azure AD Identity Protection** hoja, haga clic en **configuración**. 
4. En hello **configuración del Portal** hoja, en **las reglas de seguridad**, haga clic en **iniciar sesión en riesgo**.
5. En Hola ** iniciar sesión en riesgo ** hoja, seleccione **en** en **Habilitar regla**. 
6. Seleccione una de las siguientes opciones de hello:
   
   a. tooblock, seleccione **medio** en **bloque iniciar sesión en**
   
   b. cambio de contraseña segura tooenforce, seleccione **medio** en **requerir la autenticación multifactor**.
7. tooblock, seleccione medio en el bloque de inicio de sesión.
8. tooenforce la autenticación multifactor, seleccione **medio** en **requerir la autenticación multifactor**.
9. Haga clic en **Save**(Guardar).
10. Ahora puede probar el acceso condicional basado en riesgo mediante la simulación de ubicaciones desconocidas de Hola o IP anónima el riesgo de eventos porque son ambos **medio** el riesgo de eventos.


![Guía de](./media/active-directory-identityprotection-playbook/200.png "Guía")


## <a name="see-also"></a>Otras referencias
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

