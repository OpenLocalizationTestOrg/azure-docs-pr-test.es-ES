---
title: "aaaYou no se puede llegar allí desde aquí en hello portal de Azure desde un dispositivo Windows | Documentos de Microsoft"
description: "Obtenga información donde no existe desde aquí proceden de get y lo que podría comprobar tooavoid ejecutando en este cuadro de diálogo."
services: active-directory
keywords: acceso condicional basado en dispositivo, registro de dispositivo, habilitar registro de dispositivo, registro de dispositivo y MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>No puede llegar ahí desde aquí en un dispositivo Windows

Durante un intento de, por ejemplo, acceder a la intranet de SharePoint Online de su organización puede llegar a una página que indique que *no se puede llegar a ese sitio desde este otro*. Está viendo esta página, porque el administrador ha configurado una directiva de acceso condicional que impide que los recursos de la organización de acceso tooyour bajo ciertas condiciones. Aunque puede que sea necesario toocontact departamento de soporte técnico o el tooget de administrador que resuelve este problema, hay algunas cosas que puede probar usted mismo, en primer lugar.

Si usas un **Windows** dispositivo, debe comprobar Hola siguientes:

- ¿Usa un explorador compatible?

- ¿Ejecuta una versión compatible de Windows en el dispositivo?

- ¿Es compatible con el dispositivo?






## <a name="supported-browser"></a>Explorador compatible

Si el administrador ha configurado una directiva de acceso condicional, solo puede acceder a los recursos de su organización mediante un explorador compatible. En los dispositivos con Windows, solo se admiten **Internet Explorer** y **Edge**.

Puede identificar fácilmente si no se puede tener acceso a un recurso debido explorador incompatible tooan examinando Hola detalles de la sección de página de error de hello:

![Mensaje "No se puede llegar allí desde aquí" para exploradores no admitidos](./media/active-directory-conditional-access-device-remediation/02.png "Escenario")

corrección de Hello solo es toouse un explorador que admite la aplicación hello para la plataforma de dispositivos. Para obtener una lista completa de los exploradores compatibles, consulte la sección [Exploradores compatibles](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).  


## <a name="supported-versions-of-windows"></a>Versiones compatibles de Windows

deben cumplirse los siguientes Hola sobre el sistema de operativo de Windows hello en el dispositivo: 

- Si se ejecuta un sistema operativo de escritorio Windows en el dispositivo, debe toobe Windows 7 o posterior.
- Si se ejecuta un sistema operativo de Windows server en el dispositivo, debe toobe Windows Server 2008 R2 o posterior. 


## <a name="compliant-device"></a>Dispositivos compatible

El administrador podría haber configurado una directiva de acceso condicional que permite que los recursos de la organización de acceso tooyour solo desde dispositivos compatibles. toobe compatible, que el dispositivo debe ser cualquier tooyour unido a Active Directory local o unido tooyour Azure Active Directory.

Puede identificar fácilmente si no se puede tener acceso a un recurso debido tooa dispositivo que no es compatible con examinando Hola detalles de la sección de página de error de hello:
 
![Mensajes del tipo "No se puede llegar allí desde aquí" para dispositivos no registrados](./media/active-directory-conditional-access-device-remediation/01.png "Escenario")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>¿Es su tooan dispositivo unido a Active Directory local?

**Si el dispositivo se une tooan en Active Directory local en su organización:**

1. Asegúrese de que inicie sesión en tooWindows mediante su cuenta profesional (su cuenta de Active Directory).
2. Conectar tooyour la red corporativa a través de una red privada virtual (VPN) o DirectAccess.
3. Cuando se haya conectado, presione la tecla del logotipo de Windows hello + toolock clave Hola L su sesión de Windows.
4. Desbloquee la sesión de Windows, para lo que debe especificar las credenciales de su cuenta profesional.
5. Espere un minuto y, a continuación, vuelva a intentarlo tooaccess Hola aplicación o servicio.
6. Si ve Hola misma página, haga clic en hello **detalles más** vincular y, a continuación, póngase en contacto con el Administrador con los detalles de Hola.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>¿Es el tooan de dispositivos no unidos a un Active Directory local?

Si el dispositivo no está unido tooan Active Directory local y ejecute Windows 10, tiene dos opciones:

* Ejecutar Azure AD Join
* Agregar el trabajo o escuela tooWindows de cuenta

Para obtener información acerca de las diferencias entre estas opciones, consulte [Uso de dispositivos de Windows 10 en el área de trabajo](active-directory-azureadjoin-windows10-devices.md).  
Si el dispositivo:

- Pertenece tooyour organización, debe ejecutar Azure AD Join.
- Es un dispositivo personal o un dispositivo Windows phone, debe agregar su trabajo o escuela tooWindows de cuenta 



#### <a name="azure-ad-join-on-windows-10"></a>Azure AD Join en Windows 10

Hello toojoin pasos son los tooAzure dispositivo AD enlazado versión Hola de Windows 10 que se ejecuta en él. versión de hello toodetermine del sistema operativo Windows 10, ejecute hello **winver** comando: 

![Versión de Windows](./media/active-directory-conditional-access-device-remediation/03.png )


**Actualización de aniversario de Windows 10 (versión 1607):**

1. Abra hello **configuración** aplicación.
2. Haga clic en **Cuentas** > **Access work or school** (Acceder a la cuenta profesional o educativa).
3. Haga clic en **Conectar**.
4. Haga clic en **unir este tooAzure dispositivo AD**.
5. Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.
6. Cierre la sesión y vuelva a iniciarla con su cuenta profesional.
7. Vuelva a intentarlo aplicación hello de tooaccess.

**Actualización de Windows de 10 de noviembre de 2015 (versión 1511):**

1. Abra hello **configuración** aplicación.
2. Haga clic en **Sistema** > **About** (Acerca de).
3. Haga clic en **Unirse a Azure AD**.
4. Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.
5. Cierre la sesión y vuelva a iniciarla con su cuenta profesional (cuenta de Azure AD).
6. Vuelva a intentarlo aplicación hello de tooaccess.


#### <a name="workplace-join-on-windows-81"></a>Workplace Join en Windows 8.1

Si el dispositivo no está unido a un dominio y ejecuta Windows 8.1, toodo una unión e inscribe en Microsoft Intune, Hola lo siguiente:

1. Abra **Configuración de PC**.
2. Haga clic en **Red** > **Área de trabajo**.
3. Haga clic en **Unir**.
4. Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.
5. Haga clic en **Activar**.
6. Vuelva a intentarlo aplicación hello de tooaccess.



#### <a name="add-your-work-or-school-account-toowindows"></a>Agregar el trabajo o escuela tooWindows de cuenta 


**Actualización de aniversario de Windows 10 (versión 1607):**

1. Abra hello **configuración** aplicación.
2. Haga clic en **Cuentas** > **Access work or school** (Acceder a la cuenta profesional o educativa).
3. Haga clic en **Conectar**.
4. Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.
5. Vuelva a intentarlo aplicación hello de tooaccess.


**Actualización de Windows de 10 de noviembre de 2015 (versión 1511):**

1. Abra hello **configuración** aplicación.
2. Haga clic en **Cuentas** > **Your accounts** (Sus cuentas).
3. Haga clic en **Add work or school account**(Agregar cuenta profesional o educativa).
4. Autenticar tooyour organización, proporcione la autenticación multifactor si se le pida y, a continuación, siga los pasos de Hola que se muestran.
5. Vuelva a intentarlo aplicación hello de tooaccess.





## <a name="next-steps"></a>Pasos siguientes
[Acceso condicional de Azure Active Directory](active-directory-conditional-access.md)

