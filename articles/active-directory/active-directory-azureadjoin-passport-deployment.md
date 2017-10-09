---
title: "aaaEnable Microsoft Windows Hello para empresas de su organización | Documentos de Microsoft"
description: "Instrucciones de implementación tooenable Microsoft Passport en su organización."
services: active-directory
documentationcenter: 
keywords: "configurar Microsoft Passport, implementación de Windows Hello para empresas"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Habilitación de Windows Hello para empresas en su organización
Después de [a conectar dispositivos Unidos a un dominio de Windows 10 con Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), Hola siguientes tooenable Microsoft Windows Hello para empresas de su organización:

1. Implementación de System Center Configuration Manager  
2. Establecer configuraciones de directiva
3. Configurar perfil de certificado de Hola  

## <a name="deploy-system-center-configuration-manager"></a>Implementación de System Center Configuration Manager
certificados de usuario de toodeploy basados en Windows Hello para claves empresariales, necesita siguiente de hello:

* **Rama actual de System Center Configuration Manager** -necesita tooinstall versión 1606 o superior. Para obtener más información, vea hello [documentación para System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) y [Blog del equipo de System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Infraestructura de clave pública (PKI)** -tooenable Microsoft Windows Hello para la empresa mediante el uso de certificados de usuario, debe tener una PKI en su lugar. Si no dispone de uno, o si no desea toouse que para los certificados de usuario, puede implementar un nuevo controlador de dominio que tiene instalado 10551 (o superior) de la compilación de Windows Server 2016. Siga los pasos de hello demasiado[instalar un controlador de dominio de réplica en un dominio existente](https://technet.microsoft.com/library/jj574134.aspx) o demasiado[instalar un nuevo bosque de Active Directory, si va a crear un nuevo entorno](https://technet.microsoft.com/library/jj574166). (Hola archivos ISO están disponibles para su descarga en [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>Establecer configuraciones de directiva
Hola tooconfigure Microsoft Windows Hello para la configuración de directiva de negocio, tienes dos opciones:

* Directiva de grupo en Active Directory 
* Hola System Center Configuration Manager 

La directiva de grupo en Active Directory es hello recomendada método tooconfigure Microsoft Windows Hello para configuraciones de directivas empresariales. 

Con System Center Configuration Manager es el método hello preferido cuando también se utiliza se toodeploy certificados. Este escenario:

* Garantiza la compatibilidad con escenarios de implementación más reciente de Hola
* Se requiere en hello cliente Windows 10 versión 1607 o superior.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Configuración de Windows Hello para empresas mediante directiva de grupo en Active Directory
**Pasos**:

1. Abra el administrador del servidor y navegue demasiado**herramientas** > **Group Policy Management**.
2. En administración de directivas de grupo, navegue toohello nodo del dominio que se corresponde el dominio toohello en el que desea tooenable Azure AD Join.
3. Haga clic con el botón derecho en **Objetos de directiva de grupo** y seleccione **Nuevo**. Asigne un nombre a su objeto de directiva de grupo; por ejemplo, Habilitar Windows Hello para empresas. Haga clic en **Aceptar**.
4. Haga clic con el botón derecho en el nuevo objeto de directiva de grupo y luego seleccione **Editar**.
5. Navegue demasiado**configuración del equipo** > **directivas** > **plantillas administrativas** > **Windows Componentes** > **Windows Hello para empresas**.
6. Haga clic con el botón derecho en **Hablitar Windows Hello para empresas** y, después, seleccione **Editar**.
7. Seleccione hello **habilitado** botón de opción y, a continuación, haga clic en **aplicar**. Haga clic en **Aceptar**.
8. Ahora puede vincular tooa ubicación de objeto de directiva de grupo de Hola de su elección. tooenable esta directiva para todos los dispositivos de Windows 10 Unidos a un dominio de hello en su organización, dominio toohello de vínculo Hola directiva de grupo. Por ejemplo:
   * Una unidad organizativa (OU) específica en Active Directory donde se encontrarán los equipos unidos a un dominio de Windows 10.
   * Un grupo de seguridad específico que contiene equipos unidos a un dominio de Windows 10 que se registrarán automáticamente en Azure AD.

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>Configuración de Windows Hello para empresas mediante System Center Configuration Manager
**Pasos**:

1. Abra hello **System Center Configuration Manager**y, a continuación, navegue demasiado**activos y cumplimiento de normas > configuración de cumplimiento > acceso a recursos de empresa > Windows Hello para perfiles de negocio**.
   
    ![Configuración de Windows Hello para empresas](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. En la barra de herramientas de hello en la parte superior de hello, haga clic en **crear Windows Hello para empresas perfil**.
   
    ![Configuración de Windows Hello para empresas](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. En hello **General** cuadro de diálogo, realizar Hola pasos:
   
    ![Configuración de Windows Hello para empresas](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. Hola **nombre** cuadro de texto, escriba un nombre para el perfil, por ejemplo, **mi perfil WHfB**.
   
    b. Haga clic en **Siguiente**.
4. En hello **Supported Platforms** cuadro de diálogo, plataformas de hello select que se aprovisionará con este Windows Hello para el perfil de negocio y, a continuación, haga clic en **siguiente**.
   
    ![Configuración de Windows Hello para empresas](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. En hello **configuración** cuadro de diálogo, realizar Hola pasos:
   
    ![Configuración de Windows Hello para empresas](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. Como valor de **Configurar Windows Hello para la empresa**, seleccione **Habilitado**.
   
    b. Como valor de **Usar un Módulo de plataforma segura (TPM)**, seleccione **Obligatorio**. 
   
    c. Como valor de **Método de autenticación**, seleccione **Basada en certificados**.
   
    d. Haga clic en **Siguiente**.
6. En hello **resumen** cuadro de diálogo, haga clic en **siguiente**.
7. En hello **finalización** cuadro de diálogo, haga clic en **cerrar**.
8. En la barra de herramientas de hello en la parte superior de hello, haga clic en **implementar**.
   
    ![Configuración de Windows Hello para empresas](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Configurar perfil de certificado de Hola
Si usas autenticación basada en certificados para la autenticación local, se necesita tooconfigure e implementa un perfil de certificado. Esta tarea requiere tooset un rol de sitio del punto de registro de certificado en System Center Configuration Manager de Hola y de servidor NDES. Para obtener más información, vea hello [requisitos previos para perfiles de certificado en Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).

1. Abra hello **System Center Configuration Manager**y, a continuación, navegue demasiado**activos y cumplimiento de normas > configuración de cumplimiento > acceso a recursos de empresa > perfiles de certificado**.
2. Seleccione una plantilla que tenga el uso mejorado de clave de inicio de sesión de la tarjeta inteligente.

En hello **inscripción de SCEP** página de perfil de certificado de hello, necesita toochoose **instalar tooPassport de trabajo se producirá un error** como hello **Key Storage Provider**.

## <a name="next-steps"></a>Pasos siguientes
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticación de identidades sin contraseñas a través de Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

