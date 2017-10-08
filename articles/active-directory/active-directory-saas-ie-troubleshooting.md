---
title: "Hola aaaTroubleshooting extensión del Panel de acceso de Azure para Internet Explorer | Documentos de Microsoft"
description: "¿Cómo toouse grupo complemento de Internet Explorer de directiva toodeploy Hola para portal mis aplicaciones de Hola."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Solución de problemas de hello extensión del Panel de acceso de Internet Explorer
En este artículo le ayudará a solucionar Hola los siguientes problemas:

* Se está tooaccess no se pueden las aplicaciones a través del portal mis aplicaciones de Hola durante el uso de Internet Explorer.
* Vea "Instalar Software" mensaje incluso si ya ha instalado software de Hola de Hola.

Si es administrador, vea también: [cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Ejecutar la herramienta de diagnóstico de Hola
Puede diagnosticar problemas de instalación con hello extensión del Panel de acceso mediante la descarga y ejecuta la herramienta de diagnóstico de hello Panel de acceso:

1. [Haga clic aquí herramienta de diagnóstico de toodownload Hola.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Archivo abierto hello y presione **extraer todo** botón.
   
    ![Presionar Extraer todo](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. A continuación, presione hello **extraer** toocontinue de botón.
   
    ![Presionar Extraer](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. herramienta de hello toorun, archivo de hello contextual denominado **AccessPanelExtensionDiagnosticTool**, a continuación, seleccione **abrir con > Microsoft Windows Script Host de**.
   
    ![Abrir con > Host de script basado en Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. A continuación, verá Hola después de la ventana de diagnóstico, que describe qué puede ser incorrecto con la instalación.
   
    ![Un ejemplo de ventana de diagnóstico de hello](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Haga clic en "**Sí**" toolet Hola corrección Hola problemas de programas que se han encontrado.
7. toosave estos cambios, cierre cada ventana de Internet Explorer y, a continuación, vuelva a abrir Internet Explorer.<br />Si todavía no se puede obtener acceso a las aplicaciones, intente Hola pasos a continuación.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Compruebe que Hola que está habilitada la extensión del Panel de acceso
tooverify que Hola extensión del Panel de acceso está habilitada en Internet Explorer:

1. En Internet Explorer, haga clic en hello **icono de engranaje** en hello superior derecho de ventana hello. Después, seleccione **Opciones de Internet**.<br />(En versiones anteriores de Internet Explorer, encontrará esta opción en **Herramientas > Opciones de Internet**.
   
    ![Vaya tooTools > Opciones de Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Haga clic en hello **programas** ficha, a continuación, haga clic en hello **administrar complementos** botón.
   
    ![Hacer clic en Administrar complementos](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. En este cuadro de diálogo, seleccione **extensión del Panel de acceso** y, a continuación, haga clic en hello **habilitar** botón.
   
    ![Hacer clic en Habilitar](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave estos cambios, se cierra cada ventana de Internet Explorer y, a continuación, vuelva a abrir Internet Explorer.

## <a name="enable-extensions-for-inprivate-browsing"></a>Habilitar extensiones para la exploración de InPrivate
Si se usa el modo de exploración de InPrivate hello:

1. En Internet Explorer, haga clic en hello **icono de engranaje** en hello superior derecho de ventana hello. Después, seleccione **Opciones de Internet**.<br />(En versiones anteriores de Internet Explorer, encontrará esta opción en **Herramientas > Opciones de Internet**.
   
    ![Un ejemplo de ventana de diagnóstico de hello](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Vaya toohello **privacidad** ficha, a continuación, **desactive** Hola casilla **deshabilitar las barras de herramientas y extensiones cuando se inicia la exploración de InPrivate**</p>
   
    ![Desactivar Deshabilitar barras de herramientas y extensiones cuando se inicie la exploración de InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave estos cambios, se cierra cada ventana de Internet Explorer y, a continuación, vuelva a abrir Internet Explorer.

## <a name="uninstall-hello-access-panel-extension"></a>Desinstalar Hola extensión del Panel de acceso
Hola toouninstall extensión del Panel de acceso del equipo:

1. En el teclado, presione hello **tecla Windows** menú de inicio de tooopen Hola. Cuando se abre el menú de hello, puede escribir cualquier cosa toodo una búsqueda. Escriba "Panel de Control" y, a continuación, abra hello **el Panel de Control** cuando aparece en los resultados de búsqueda de Hola.
   
    ![Buscar el Panel de Control](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. En hello esquina superior derecha del Panel de Control de Hola, cambie hello **ver** opción demasiado**iconos grandes**. A continuación, busque y haga clic en hello **programas y características** botón.
   
    ![Cambios Hola vista tooshow iconos grandes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. En la lista de hello, seleccione **extensión del Panel de acceso**y haga clic en Hola de hello **desinstalar** botón.
   
    ![Hacer clic en Desinstalar](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. A continuación, puede intentar extensión de hello tooinstall nuevo toosee si se ha solucionado el problema de Hola.

Si encuentra problemas al desinstalar la extensión de hello, también puede quitar mediante hello [Microsoft repararlo](https://go.microsoft.com/?linkid=9779673) herramienta.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [¿Cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](active-directory-saas-ie-group-policy.md)

