---
title: "instalar aaaProblem Hola conector del agente de Proxy de aplicación | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot emite podría Hola de cara al instalar agente conector del Proxy de aplicación"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problema al instalar el conector del agente de Proxy de aplicación Hola

Conector del Proxy de aplicación de AAD de Microsoft es un componente de dominio interno que usa conectividad de las conexiones salientes tooestablish Hola de dominio interno de la toohello del punto de conexión disponible de hello en la nube.

## <a name="general-problem-areas-with-connector-installation"></a>Áreas problemáticas generales con la instalación del conector

Cuando se produce un error en la instalación de Hola de un conector, causa Hola suele ser uno de hello siguientes áreas:

1.  **Conectividad** – toocomplete una instalación correcta, Hola nuevo conector necesidades tooregister y establecer propiedades de confianza en el futuro. Esto se realiza mediante la conexión toohello servicio Proxy de aplicación de AAD en la nube.

2.  **Establecimiento de confianza** – nuevo conector de hello crea un certificado autofirmado y registra el servicio en la nube toohello.

3.  **Autenticación de Hola, administrador** : durante la instalación, Hola usuario debe proporcionar credenciales de administrador de instalación del conector toocomplete Hola.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Compruebe el servicio de Proxy de aplicación de nube de toohello de conectividad y página Login de Microsoft

**Objetivo:** comprobar puede conectar esa máquina de conector Hola extremo de registro de Proxy de aplicación AAD de toohello, así como la página de inicio de sesión de Microsoft.

1.  Abrir un toohello de explorador y vaya después de la página web: <https://aadap-portcheck.connectorporttest.msappproxy.net> y compruebe que tooCentral de conectividad de hello EE. UU. y funciona UU centros de datos con los puertos 9090 y 9091.

2.  Si cualquiera de estos puertos no se realiza correctamente (no tiene una marca de verificación verde), compruebe que Hola Firewall o proxy de back-end tiene \*. msappproxy.net con puertos 9090 y 9091 definida correctamente.

3.  Abra un explorador (pestaña independiente) y vaya toohello después de la página web: <https://login.microsoftonline.com>, asegúrese de que puede iniciar sesión toothat página.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Comprobación de que los componentes de máquina y back-end admitan el certificado de confianza del proxy de aplicación

**Objetivo:** Compruebe que la máquina de conector de hello, el proxy de back-end y el firewall pueden admitir certificado Hola creado por el conector de Hola de confianza en el futuro.

>[!NOTE]
>Conector de Hello intenta toocreate un certificado SHA512 que es compatible con TLS 1.2. Si la máquina de Hola o proxy y firewall de back-end de hello no admite TLS 1.2, instalación de hello producirá un error.
>
>

**problema de Hola tooresolve:**

1.  Compruebe la máquina de hello es compatible con TLS 1.2: las versiones de todas las ventanas posteriores a 2012 R2 deben admitir TLS 1.2. Si el equipo del conector es de una versión de 2012 R2 o anterior, asegúrese de que ese Hola KB/s siguientes están instalados en el equipo de hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Póngase en contacto con su administrador de red y pídale que tooverify que Hola back-end proxy y firewall no bloquean SHA512 para el tráfico saliente.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Compruebe administrador es tooinstall usado Hola conector

**Objetivo:** compruebe ese usuario Hola que trate de conector de hello tooinstall es un administrador con las credenciales correctas. Actualmente, el usuario de hello debe ser un administrador global de hello toosucceed de instalación.

**las credenciales de hello tooverify son correctas:**

Conectar demasiado<https://login.microsoftonline.com> y uso Hola mismas credenciales. Asegúrese de que el inicio de sesión de hello es correcta. Puede comprobar el rol de usuario de hello yendo demasiado**Azure Active Directory**  - &gt; **usuarios y grupos**  - &gt; **todos los usuarios**. 

Seleccione su cuenta de usuario, a continuación, "Directory Role" en el menú resultante Hola. Compruebe que ese rol seleccionado hello es "Administrador Global". Si es que no se puede tooaccess cualquiera de hello páginas a lo largo de estos pasos, no es un administrador global.

## <a name="next-steps"></a>Pasos siguientes
[Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
