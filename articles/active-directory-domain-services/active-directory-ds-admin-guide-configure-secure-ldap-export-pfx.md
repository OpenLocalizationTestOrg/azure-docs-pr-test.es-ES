---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services

## <a name="before-you-begin"></a>Antes de empezar
Asegúrese de haber completado la [Tarea 1: Obtención de un certificado para LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Tarea 2: exportar hello tooa de certificado LDAP seguro. Archivo PFX
Antes de iniciar esta tarea, asegúrese de que ha obtenido el certificado LDAP seguro de Hola de una entidad de certificación pública o que ha creado un certificado autofirmado.

Realizar pasos de hello, tooexport Hola LDAPS certificados tooa. Archivo PFX.

1. Hola presione **iniciar** botón y escriba **R**. Hola **ejecutar** cuadro de diálogo, escriba **mmc** y haga clic en **Aceptar**.

    ![Iniciar la consola de MMC de Hola](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. En hello **User Account Control** símbolo del sistema, haga clic en **Sí** toolaunch MMC (Microsoft Management Console) como administrador.
3. De hello **archivo** menú, haga clic en **agregar o quitar complemento...** .

    ![Agregar la consola de complemento tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. Hola **agregar o quitar complementos** cuadro de diálogo, seleccione hello **certificados** complemento y haga clic en hello **Agregar >** botón.

    ![Agregar la consola de complemento tooMMC de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. Hola **complemento certificados** asistente, seleccione **cuenta de equipo** y haga clic en **siguiente**.

    ![Adición del complemento Certificados a la cuenta de equipo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. En hello **Seleccionar equipo** , seleccione **equipo Local: (equipo de Hola que se está ejecutando esta consola)** y haga clic en **finalizar**.

    ![Adición del complemento Certificados: seleccionar equipo](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. Hola **agregar o quitar complementos** cuadro de diálogo, haga clic en **Aceptar** tooadd tooMMC de complemento de certificados de Hola.

    ![Agregar certificados complemento tooMMC - terminado](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. En la ventana MMC de hello, haga clic en tooexpand **raíz de consola**. Debería ver Hola complemento certificados cargado. Haga clic en **certificados (equipo Local)** tooexpand. Haga clic en hello tooexpand **Personal** nodo, seguido por hello **certificados** nodo.

    ![Abrir el almacén de certificados personal](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Debería ver el certificado autofirmado Hola que hemos creado. Puede examinar propiedades Hola de hello certificado tooensure Hola huella digital coincidencias que notificar en windows PowerShell de hello al crear el certificado de Hola.
10. Seleccione Hola certificado autofirmado y **haga**. En el menú contextual de hello, seleccione **todas las tareas** y seleccione **exportar...** .

    ![Exportación de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. Hola **Asistente para exportar certificados**, haga clic en **siguiente**.

    ![Asistente para exportación de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. En hello **exportar la clave privada** página, seleccione **Sí, exportar la clave privada de hello**y haga clic en **siguiente**.

    ![Exportación de certificados: clave privada](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > DEBE exportar la clave privada de hello junto con el certificado de Hola. Si proporcionas PFX que no contiene la clave privada de hello certificado de Hola, habilitación de LDAP seguro para el dominio administrado produce un error.
    >
    >
13. En hello **Exportar formato de archivo** página, seleccione **intercambio de información Personal: PKCS #12 (. PFX)** como formato de archivo de Hola para hello certificado exportado.

    ![Exportación de certificados: formato de archivos](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Solo Hola. Se admite el formato de archivo PFX. No exporte Hola certificado toohello. Formato de archivo CER.
    >
    >
14. En hello **seguridad** página, seleccione hello **contraseña** opción y escriba un hello tooprotect de contraseña. Archivo PFX. Recuerde esta contraseña porque lo necesitará en la siguiente tarea de Hola. Haga clic en **siguiente** tooproceed.

    ![Contraseña para la exportación de certificados ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Anote esta contraseña. Se necesita al habilitar LDAP seguro para este dominio administrado en [tarea 3: habilitar LDAP seguro para el dominio administrado Hola](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. En hello **tooExport archivo** página, especifique el nombre de archivo de Hola y la ubicación que desee que el certificado de hello tooexport.

    ![Ruta para la exportación de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. En hello después de la página, haga clic en **finalizar** archivo PFX de tooexport Hola certificado tooa. Debería ver el cuadro de diálogo de confirmación cuando se ha exportado el certificado de Hola.

    ![Exportación de certificados: listo](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Paso siguiente
[Tarea 3: habilitar LDAP seguro para el dominio administrado Hola](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
