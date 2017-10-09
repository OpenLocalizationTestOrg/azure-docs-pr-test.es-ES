---
title: "interfaz de usuario de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe la interfaz de usuario de administrador de instantáneas StorSimple hello y explica cómo toouse lo hello y trabajos de copia de seguridad de toomanage catálogo de copia de seguridad."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>Trabajos de copia de seguridad de toomanage de interfaz de usuario de administrador de instantáneas de StorSimple de uso y el catálogo de copia de seguridad

## <a name="overview"></a>Información general
Hola, Administrador de instantáneas StorSimple tiene una interfaz de usuario intuitiva que puede usar tootake y administrar copias de seguridad. Este tutorial proporciona una interfaz de usuario de toohello de introducción y, a continuación, se explica cómo toouse de componentes de Hola. Para obtener una descripción detallada de hello StorSimple Snapshot Manager, consulte [¿qué es el Administrador de instantáneas StorSimple?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Descripción de la consola
usuario de hello tooview de la interfaz, haga clic en el icono de administrador de instantáneas de StorSimple de hello en el escritorio. aparece en la ventana de consola de Hello, como se muestra en hello siguiente ilustración.

![Paneles de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

ventana de la consola de Hello tiene cinco elementos principales. Haga clic en el vínculo apropiado de Hola para obtener una descripción completa de cada elemento.

* [Barra de menús](#menu-bar) 
* [Barra de herramientas](#tool-bar) 
* [Panel de Ámbito](#scope-pane) 
* [Panel de Resultados](#results-pane) 
* [Panel de Acciones](#actions-pane) 

Además, hello es compatible con el Administrador de instantáneas StorSimple [navegación y un número de métodos abreviados de teclado](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Accesibilidad de la consola
interfaz de usuario de administrador de instantáneas StorSimple Hello es compatible con características de accesibilidad de hello proporcionadas por sistema operativo de Windows de Hola y Hola Microsoft Management Console (MMC), así como algunos métodos abreviados de teclado de administrador de instantáneas StorSimple específicos. 

* Para obtener una descripción de las características de accesibilidad de Windows hello, vaya demasiado[métodos abreviados de teclado para Windows](https://support.microsoft.com/kb/126449). 
* Para obtener una descripción de las características de accesibilidad MMC de hello, vaya demasiado[accesibilidad para MMC 3.0](https://technet.microsoft.com/library/cc766075.aspx)
* Para obtener una descripción de las características de accesibilidad de hello StorSimple Snapshot Manager, vaya demasiado[navegación y accesos directos de teclado](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Barra de menús
barra de menús de Hello en parte superior de Hola de ventana de la consola de hello contiene [archivo](#file-menu), [acción](#action-menu), [vista](#view-menu), [favoritos](#favorites-menu), [ventana ](#window-menu), y [ayuda](#help-menu) menús.

Haga clic en cualquier elemento de toosee de barra de menús de hello una lista de comandos disponibles en ese menú. Hello en el ejemplo siguiente se muestra hello **vista** menú seleccionado en la barra de menús de Hola.

![Menú Vista seleccionado](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>Menú Archivo
Hola **archivo** menú contiene comandos estándar de Microsoft Management Console (MMC).

#### <a name="menu-access"></a>Acceso al menú
Hola tooview **archivo** menú, haga clic en **archivo** en la barra de menús de Hola. Hola después de menú aparece.

![Menú Archivo de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Descripción del menú
Hello tabla siguiente describen los elementos que aparecen en hello **archivo** menú.

| Elemento de menú | Descripción |
|:--- |:--- |
| Nuevo |Haga clic en **New** toocreate una nueva consola en función de hello StorSimple Snapshot Manager. |
| Abrir |Haga clic en **abiertos** tooopen una consola existente. |
| Save |Haga clic en **guardar** consola actual de toosave Hola. |
| Guardar como |Haga clic en **Guardar como** toocreate una nueva instancia de la consola actual Hola cuyo nombre ha cambiado. Hola de uso **Guardar como** opción toocustomize una vista y guardarla para su recuperación posterior. Por ejemplo, podría crear complementos Administrador de instantáneas StorSimple ese servidor de punto de toospecific. |
| Agregar o quitar complemento |Haga clic en **agregar o quitar complemento** tooadd o quitar complementos y tooorganize nodos hello **ámbito** panel. Para obtener más información, consulte demasiado[agregar, quitar y organizar complementos y extensiones en MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Opciones |Haga clic en **opciones** el icono de la consola de hello toochange, especifica los modos de acceso de usuario y los permisos o eliminar espacio en disco disponible tooincrease consola archivos. |
| Lista de rutas de acceso |Haga clic en una ruta de acceso en hello numerado lista tooreopen un archivo que ha abierto recientemente. |
| Salir |Haga clic en **Exit** tooclose hello **archivo** menú. |

### <a name="action-menu"></a>Menú Acción
Hola de uso **acción** tooselect del menú de acciones disponibles. Hola elementos disponibles tooyou dependen de la selección de Hola que realice en hello **ámbito** panel o **resultados** panel.

#### <a name="menu-access"></a>Acceso al menú
Hola tooview **acción** menú, realice uno de hello siguientes:

* Haga clic en un elemento de hello **ámbito** panel o **resultados** panel.
* Seleccione un elemento de hello **ámbito** panel o **resultados** panel y, a continuación, haga clic en **acción** en la barra de menús de Hola. 

Por ejemplo, si selecciona el nodo superior de Hola Hola **ámbito** panel y, a continuación, haga clic o pulse **acción** en la barra de menús de hello, hello aparecerá siguiente menú.

![Menú Acción de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Hola **acciones** panel (Hola derecha de la consola de hello) contiene Hola misma lista de acciones que hello **acción** menú. Además, Hola **acciones** panel contiene Hola **vista** opciones de menú, lo que permite una vista personalizada de hello toocreate **resultados** panel.

![Panel de Acciones con el menú Vista abierto](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Descripción del menú
Hello en la tabla siguiente contiene una lista alfabética de acciones de administrador de instantáneas StorSimple. 

* Hola **acción** columna muestra las acciones que puede realizar en los nodos y sus resultados. 
* Hola **navegación** columna explica cómo Hola adecuado toodisplay **acción** menú para que pueda seleccionar acción de Hola. Algunas acciones aparecen en varios menús **Acción** . Para estas acciones, seleccione una **navegación** opción de lista con viñetas Hola. 
* Hola **descripción** columna describe cómo toouse cada acción en hello **acción** menú o panel de acciones y explica lo que hace.

> [!NOTE]
> Hola **acciones** panel y **acción** menús contienen opciones adicionales, como **vista**, **nueva ventana desde aquí**,  **Actualizar**, **Exportar lista**, y **ayuda**. Estas opciones están disponibles como parte del programa Hola a MMC y no son específico tooStorSimple Administrador de instantáneas. tabla de Hello incluye descripciones de estas opciones.
> 
> 

| Acción | Navegación | Descripción |
|:--- |:--- |:--- |
| Autenticar |Haga clic en hello **dispositivos** nodo y menú contextual de un dispositivo en hello **resultados** panel. |Haga clic en **Authenticate** contraseña de hello tooenter que ha configurado para el dispositivo de Hola. |
| Clon |Expanda **catálogo de copia de seguridad**, expanda **instantáneas en la nube**, haga clic en una copia de seguridad con fecha y, a continuación, seleccione un volumen en hello **resultados** panel. |Haga clic en **clon** toocreate una copia de una nube de instantáneas y almacenarlo en una ubicación que desee. |
| Configurar un dispositivo |Menú contextual hello **dispositivos** nodo. |Haga clic en **configurar un dispositivo** tooconfigure un único dispositivo o host de varios dispositivos tooconnect toohello Windows. |
| Crear directiva de copia de seguridad |Siga uno de los procedimientos de hello:<ul><li>Haga clic con el botón derecho en **Directivas de copia de seguridad**.</li><li>Haga clic o expanda **Grupos de volúmenes** y, a continuación, haga clic en un grupo de volúmenes.</li><li>Haga clic o expanda **Catálogo de copias de seguridad** y, a continuación, haga clic en un grupo de volúmenes.</li></ul> |Haga clic en **Crear directiva de copia de seguridad** tooconfigure copias de seguridad programadas para un grupo de volúmenes. |
| Crear grupo de volúmenes |Siga uno de los procedimientos de hello:<ul><li>Haga clic en hello **volúmenes** nodo y, a continuación, haga un volumen en hello **resultados** panel.</li><li>Menú contextual hello **grupos de volúmenes** nodo.</li></ul> |Haga clic en **crear grupo de volúmenes** grupo de volúmenes de tooassign volúmenes tooa. |
| Eliminar |Haga clic en un nodo o resultado (este elemento aparece en muchos menús **Acción** y paneles de **Acciones**). |Haga clic en **eliminar** toodelete Hola nodo o resultado seleccionado. Cuando aparezca el cuadro de diálogo de confirmación de hello, confirmar o cancelar la eliminación de Hola. |
| Detalles |Haga clic en hello **dispositivos** nodo y, a continuación, haga un dispositivo en hello **resultados** panel. |Haga clic en **detalles** detalles de configuración de hello toosee para un dispositivo. |
| Edit |Haga clic en **directivas de copia de seguridad**y, a continuación, haga clic en una directiva en hello **resultados** panel. |Haga clic en **editar** programación de copia de seguridad de hello toochange para un grupo de volúmenes. |
| Exportar lista |Haga clic en cualquier nodo o resultado (este elemento aparece en todos los menús **Acción** y paneles de **Acciones**). |Haga clic en **Exportar lista** toosave una lista en un archivo de valores separados por comas (CSV). A continuación, puede importar este archivo en una aplicación de hoja de cálculo para su análisis. |
| Ayuda |Haga clic en cualquier nodo o resultado. (Este elemento aparece en todos los menús **Acción** y paneles de **Acciones**). |Haga clic en **ayuda** tooopen ayuda en pantalla en otra ventana del explorador. |
| Nueva ventana desde aquí |Haga clic en cualquier nodo o resultado (este elemento aparece en todos los menús **Acción** y paneles de **Acciones**). |Haga clic en **nueva ventana desde aquí** tooopen una nueva ventana del Administrador de instantáneas StorSimple. |
| Actualizar |Haga clic en cualquier nodo o resultado (este elemento aparece en todos los menús **Acción** y paneles de **Acciones**). |Haga clic en **actualizar** ventana de administrador de instantáneas de StorSimple de tooupdate Hola que se muestra actualmente. |
| Actualizar dispositivo |Haga clic en hello **dispositivos** nodo y menú contextual de un dispositivo en hello **resultados** panel. |Haga clic en **actualizar dispositivo** toosynchronize un dispositivo conectado específico con el Administrador de instantáneas de StorSimple. |
| Actualizar dispositivos |Menú contextual hello **dispositivos** nodo. |Haga clic en **actualizar dispositivos** toosynchronize la lista de dispositivos conectados con el Administrador de instantáneas de StorSimple. |
| Volver a examinar volúmenes |Menú contextual hello **volúmenes** nodo. |Haga clic en **volver a examinar volúmenes** tooupdate lista de Hola de volúmenes que aparece en hello **resultados** panel. |
| Restauración |Expanda el **Catálogo de copias de seguridad**, un grupo de volúmenes y luego **Instantáneas locales** o **Instantáneas de nube**; a continuación, haga clic con el botón derecho en una copia de seguridad. |Haga clic en **restaurar** tooreplace Hola actual grupo datos del volumen con los datos de Hola de copia de seguridad seleccionada de Hola. |
| Realizar copia de seguridad |Siga uno de los procedimientos de hello:<ul><li>Expanda **Grupos de volúmenes** y, a continuación, haga clic en un grupo de volúmenes.</li><li>Expanda **Catálogo de copias de seguridad** y, a continuación, haga clic en un grupo de volúmenes.</li></ul> |Haga clic en **hacer copia de seguridad** toostart un trabajo de copia de seguridad inmediatamente. |
| Alternar visualización de importaciones |Nodo superior de contextual Hola Hola **ámbito** panel (hello **StorSimple Snapshot Manager** nodo en los ejemplos de hello). |Haga clic en **alternar visualización de importaciones** tooshow u ocultar grupos de volúmenes de Hola y copias de seguridad asociadas que se importaron desde Hola panel de servicio de administrador de dispositivos de StorSimple. |

### <a name="view-menu"></a>Menú Vista
Hola de uso **vista** menú toocreate una vista personalizada de hello **resultados** contenido del panel. Hola **vista** menú contiene **agregar o quitar columnas** y **personalizar** opciones.

#### <a name="menu-access"></a>Acceso al menú
Puede tener acceso a hello **vista** menú en la barra de menús de Hola o hello **acciones** panel.

![Menú Vista de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Descripción del menú
Hello tabla siguiente describen los elementos que aparecen en hello **vista** menú.

| Elemento de menú | Descripción |
|:--- |:--- |
| Agregar o quitar columnas |Haga clic en **agregar o quitar columnas** tooadd o quitar columnas de hello **resultados** panel. |
| Personalizar |Haga clic en **personalizar** tooshow u ocultar elementos en la ventana de consola de administrador de instantáneas StorSimple Hola. |

### <a name="favorites-menu"></a>Menú Favoritos
Usar hello **favoritos** menú tooadd, quitar y organizar las vistas de página y las tareas que utilizan con frecuencia. 

#### <a name="menu-access"></a>Acceso al menú
Puede tener acceso a hello **favoritos** menú en la barra de menús de Hola.

![Menú Favoritos de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Descripción del menú
Hello tabla siguiente describen los elementos que aparecen en hello **favoritos** menú.

| Elemento de menú | Descripción |
|:--- |:--- |
| Agregar tooFavorites |Haga clic en **agregar tooFavorites** tooadd Hola actual ver tooyour lista de favoritos. |
| Organizar Favoritos |Haga clic en **Organizar favoritos** contenido de hello tooorganize de la carpeta de favoritos. |

### <a name="window-menu"></a>Menú Ventana
Hola de uso **ventana** ventanas de consola de administrador de instantáneas de StorSimple de tooadd y reorganizar menú.

#### <a name="menu-access"></a>Acceso al menú
Puede tener acceso a hello **ventana** menú en la barra de menús de Hola.

![Menú Ventana de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

lista numerada de Hello final Hola del menú de hello muestra hello ventanas que están abiertas. Haga clic en cualquier ventana en la ventana de lista toobring hello en primer plano de Hola. 

#### <a name="menu-description"></a>Descripción del menú
Hello tabla siguiente describen los elementos de Hola que aparecen en el menú de la ventana de Hola.

| Elemento de menú | Descripción |
|:--- |:--- |
| Nueva ventana |Haga clic en **nueva ventana** tooopen una nueva ventana de consola (en la ventana existente de suma toohello). |
| En cascada |Haga clic en **Cascade** toodisplay ventanas de consola abiertas hello en cascada. |
| Mosaico horizontal |Haga clic en **mosaico horizontal** toodisplay ventanas de consola abiertas hello en un formato de mosaico (o cuadrícula). |
| Organizar iconos |Si tiene varios consola de windows abren y repartidas por el escritorio, minimícelas y, a continuación, haga clic en **Organizar iconos** tooarrange usarlas en una fila horizontal en la parte inferior de saludo de la pantalla. |

### <a name="help-menu"></a>Menú Ayuda
Hola de uso **ayuda** ayuda en pantalla de menú tooview disponible para hello MMC y Administrador de instantáneas StorSimple. También puede ver información acerca de hello MMC y Administrador de instantáneas StorSimple versiones de software que están instalados actualmente en el sistema. 

Puede tener acceso a hello **ayuda** menú en la barra de menús de Hola. También puede tener acceso a los temas de Ayuda de administrador de instantáneas StorSimple de hello **acciones** panel.

![Menú Ayuda de Administrador de instantáneas StorSimple](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Descripción del menú
Hello en la tabla siguiente describe los elementos que aparecen en el menú Ayuda de Hola.

| Elemento de menú | Descripción |
|:--- |:--- |
| Ayuda de Administrador de instantáneas StorSimple |Haga clic en **ayuda en el Administrador de instantáneas de StorSimple** tooopen ayuda de administrador de instantáneas de StorSimple en una ventana independiente. |
| Temas de Ayuda |Haga clic en **temas de Ayuda** ayuda en pantalla de MMC tooopen en una ventana independiente. |
| Sitio Web de TechCenter |Haga clic en **sitio Web de TechCenter** tooopen Hola Microsoft TechNet Tech Center portada en una ventana independiente. |
| Acerca de Microsoft Management Console |Haga clic en **sobre Microsoft Management Console** toosee Hola a qué versión de Microsoft Management Console está instalada en el sistema. |
| Acerca de Administrador de instantáneas StorSimple |Haga clic en **sobre el Administrador de instantáneas de StorSimple** toosee qué versión del complemento de hello está instalada en el sistema. |

## <a name="tool-bar"></a>Barra de herramientas
barra de herramientas de Hello, situada debajo de la barra de menús de hello, contiene navegación e iconos de la tarea. Cada icono es una tarea específica de tooa de método abreviado.

### <a name="icon-descriptions"></a>Descripciones de los iconos
Hello tabla siguiente describen los iconos de Hola que aparecen en la barra de herramientas de Hola. 

| Icono | Descripción |
|:--- |:--- |
| ![Flecha izquierda](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Haga clic en la página anterior del toohello de tooreturn de icono de flecha izquierda para saludo. |
| ![Flecha derecha](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Haga clic en la página siguiente de hello flecha derecha toogo toohello (si Hola flecha está en gris, acción de hello no está disponible). |
| ![Icono de subir](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Haga clic en hello una toogo icono Subir un nivel en el árbol de consola de hello (hello **ámbito** panel). |
| ![Mostrar u ocultar el árbol de consola](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Haga clic en hello mostrar/ocultar consola árbol icono tooshow u ocultar hello **ámbito** panel. |
| ![Exportar lista](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Haga clic en hello Exportar lista icono tooexport un archivo CSV de tooa de lista que especifique. |
| ![Icono de ayuda](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Haga clic en hello ayuda icono tooopen un tema de ayuda en pantalla de MMC. |
| ![Mostrar u ocultar el panel Acciones](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Haga clic en Mostrar u ocultar de hello **acciones** Hola de tooshow u ocultar del icono de panel **acciones** panel. |

## <a name="scope-pane"></a>Panel de Ámbito
Hola **ámbito** panel es Hola panel situado en hello UI del Administrador de instantáneas StorSimple. Contiene el árbol de consola (o nodo) de Hola y es el mecanismo de navegación principal de hello para el Administrador de instantáneas de StorSimple. 

### <a name="scope-pane-structure"></a>Estructura del panel Ámbito
Hola **ámbito** panel contiene una serie de objetos seleccionables (nodos) que se organizan en una estructura de árbol. 

![Panel de Ámbito](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand o contraer un nodo, haga clic en icono de flecha Hola siguiente nombre de nodo toohello.
* estado de hello tooview o los contenidos de un nodo, haga clic en el nombre del nodo de Hola. información de Hello aparece en hello **resultados** panel. 

Hola **ámbito** panel contiene Hola siguientes nodos: 

* [Nodo Dispositivos](#devices-node) 
* [Nodo Volúmenes](#volumes-node) 
* [Nodo Grupos de volúmenes](#volume-groups-node) 
* [Nodo de Directivas de copia de seguridad](#backup-policies-node) 
* [Nodo Catálogo de copias de seguridad](#backup-catalog-node) 
* [Nodo Trabajos](#jobs-node) 

### <a name="scope-pane-tasks"></a>Tareas del panel Ámbito
Puede usar hello **ámbito** panel toocomplete una acción en un nodo específico. tooselect una tarea, siga uno de los procedimientos de hello:

* Haga clic en el nodo de hello y, a continuación, seleccione una tarea de Hola de menú de Hola que aparece.
* Haga clic en el nodo de hello y, a continuación, haga clic en **acción** en la barra de menús de Hola. Seleccione una tarea de Hola de menú de Hola que aparece.
* Haga clic en el nodo de Hola y acción de hello, a continuación, seleccione en hello **acciones** panel.

Al seleccionar un nodo y usar cualquiera de estos métodos toosee una lista de tareas, se muestran solo aquellas acciones que se pueden realizar en ese nodo.

### <a name="devices-node"></a>Nodo Dispositivos
Hola **dispositivos** nodo representa dispositivos de StorSimple de Hola y StorSimple dispositivos virtuales que están conectado tooStorSimple Administrador de instantáneas. Seleccione este nodo tooconnect y configurar un dispositivo e importar sus volúmenes asociados, grupos de volúmenes y copias de seguridad existentes. Varios dispositivos pueden ser un único host tooa conectado.

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**dispositivos**.
* toosee un menú de acciones disponibles, haga clic en hello **dispositivos** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de dispositivos configurados, haga clic en **dispositivos** en hello **ámbito** panel. lista de Hola de dispositivos, junto con información sobre cada dispositivo aparece en hello **resultados** panel.

### <a name="volumes-node"></a>Nodo Volúmenes
Hola **volúmenes** nodo representa las unidades de Hola que corresponden toohello montadas por host hello, incluidos aquellos detectados a través de iSCSI y detectados a través de un dispositivo. Use esta lista de nodo tooview Hola de volúmenes disponibles y asignar volúmenes individuales toovolume grupos.

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**volúmenes**.
* toosee un menú de acciones disponibles, haga clic en hello **volúmenes** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de volúmenes, haga clic en **volúmenes** en hello **ámbito** panel. lista de Hola de volúmenes, junto con información acerca de cada volumen, aparece en hello **resultados** panel.

### <a name="volume-groups-node"></a>Nodo Grupos de volúmenes
Los grupos de volúmenes también conocen como grupos de consistencia. Cada grupo de volúmenes es un conjunto de volúmenes relacionados con las aplicaciones que le ayuda a tooensure coherencia con las aplicaciones durante las operaciones de copia de seguridad. Hola de uso **grupos de volúmenes** nodo tooconfigure estos grupos y las copias de seguridad interactivo de tootake o crear programaciones de copia de seguridad. 

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**grupos de volúmenes**.
* toosee un menú de acciones disponibles, haga clic en hello **grupos de volúmenes** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de grupos de volúmenes, haga clic en **grupos de volúmenes** en hello **ámbito** panel. lista de Hola de grupos de volúmenes, junto con información sobre cada grupo de volúmenes, aparece en hello **resultados** panel.

### <a name="backup-policies-node"></a>Nodo de Directivas de copia de seguridad
Las directivas de copia de seguridad son las programaciones de trabajo para realizar instantáneas locales y en la nube. Hola de uso **directivas de copia de seguridad** toospecify de nodo con qué frecuencia se crea una copia de seguridad y cuánto tiempo debe ser una copia de seguridad conservan. 

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**directivas de copia de seguridad**.
* toosee un menú de acciones disponibles, haga clic en hello **directivas de copia de seguridad** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de directivas de copia de seguridad, haga clic en **directivas de copia de seguridad** en hello **ámbito** panel. lista de Hola de directivas de copia de seguridad, junto con información sobre cada directiva, aparece en hello **resultados** panel.

> [!NOTE]
> Puede conservar un máximo de 64 copias de seguridad.


### <a name="backup-catalog-node"></a>Nodo Catálogo de copias de seguridad
Hola **catálogo de copia de seguridad** nodo contiene listas de copias de seguridad en el sitio y fuera de las instalaciones de volúmenes de StorSimple de Azure. Este nodo se organiza por grupo de volúmenes, y cada contenedor de grupo de volúmenes contiene estructuras separadas para las instantáneas locales (hello **instantánea Local**nodo s) y en la nube (hello **instantáneas en la nube** nodo ). Cuando se expande, cada contenedor de grupo de volúmenes enumera todos los Hola copias de seguridad correctas que se tomaron interactivamente o mediante una directiva configurada.

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**catálogo de copia de seguridad**.
* toosee un menú de acciones disponibles, haga clic en hello **catálogo de copia de seguridad** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de instantáneas de copia de seguridad, haga clic en **catálogo de copia de seguridad** en hello **ámbito** panel. lista de Hola de instantáneas, junto con información sobre cada instantánea, aparece en hello **resultados** panel.

### <a name="local-snapshots-node"></a>Nodo Instantáneas locales
Hola **instantáneas locales** nodo enumera las instantáneas locales para un grupo de volúmenes específico. nodo de Hola se encuentra en hello **catálogo de copia de seguridad** nodo Hola **ámbito** panel. Las instantáneas locales son copias instantáneas de datos del volumen que se almacenan en el dispositivo de StorSimple de Azure de Hola. Normalmente, este tipo de copia de seguridad se puede crear y restaurar rápidamente. Puede usar una instantánea local como lo haría con una copia de seguridad local.

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**instantáneas locales**.
* toosee un menú de acciones disponibles, haga clic en hello **instantáneas locales** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de las instantáneas locales, haga clic en **instantáneas locales** en hello **ámbito** panel. lista de Hola de instantáneas, junto con información sobre cada instantánea, aparece en hello **resultados** panel.

### <a name="cloud-snapshots-node"></a>Nodo Instantáneas de nube
Hola **instantáneas en la nube** nodo enumera las instantáneas de nube para un grupo de volúmenes específico. nodo de Hola se encuentra en hello **catálogo de copia de seguridad** nodo Hola **ámbito** panel. Las instantáneas de nube son copias instantáneas de datos del volumen que se almacenan en la nube de Hola. Una instantánea en la nube es equivalente instantánea de tooa replicada en un sistema de almacenamiento diferente, fuera del sitio. Las instantáneas en la nube son especialmente útiles en escenarios de recuperación ante desastres.

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**instantáneas en la nube**.
* toosee un menú de acciones disponibles, haga clic en hello **instantáneas en la nube** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de instantáneas en la nube, haga clic en **instantáneas en la nube** en hello **ámbito** panel. lista de Hola de instantáneas, junto con información sobre cada instantánea, aparece en hello **resultados** panel.

### <a name="jobs-node"></a>Nodo Trabajos
Hola **trabajos** nodo contiene información acerca de los trabajos de copia de seguridad programadas, en ejecución y recientemente completados. 

* nodo de hello tooexpand, haga clic en icono de flecha de hello siguiente demasiado**trabajos**.
* toosee un menú de acciones disponibles, haga clic en hello **trabajos** nodo o menú contextual cualquiera de los nodos de Hola que aparecen en hello vista expandida.
* toosee una lista de los trabajos programados, expanda hello **trabajos** nodo y, a continuación, haga clic en **programada**. Hello lista de los trabajos previamente configurados e información sobre cada trabajo aparece en hello **resultados** panel. 
* toosee una lista de trabajos completados recientemente, expanda hello **trabajos** nodo y, a continuación, haga clic en **últimas 24 horas**. Aparece una lista de trabajos que se completaron en hello últimas 24 horas en hello **resultados** panel. Hola **resultados** panel también contiene información sobre cada trabajo completado.
* toosee una lista de trabajos que se están ejecutando, expanda hello **trabajos** nodo y, a continuación, haga clic en **ejecutando**. lista de Hola de trabajos e información sobre cada trabajo en ejecución actualmente aparece en hello **resultados** panel.

## <a name="results-pane"></a>Panel de Resultados
Hola **resultados** panel es el panel de centro de Hola Hola UI del Administrador de instantáneas StorSimple. Contiene listas e información de estado detallada de nodo de Hola que seleccionó en hello **ámbito** panel.

### <a name="example"></a>Ejemplo
Hola toosee siguiente ejemplo, haga clic en hello **grupos de volúmenes** nodo Hola **ámbito** panel. Hola **resultados** panel muestra una lista de grupos de volúmenes con detalles acerca de cada grupo.

![Panel de Resultados](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Puede configurar los detalles de hello mostrados en hello **resultados** panel: haga clic en un nodo en hello **ámbito** panel, haga clic en **vista**y, a continuación, haga clic en **agregar o quitar Columnas**.

## <a name="actions-pane"></a>Panel de Acciones
Hola **acciones** panel es el panel derecho de Hola Hola UI del Administrador de instantáneas StorSimple. Contiene un menú de las operaciones que puede realizar en el nodo de hello, vista o datos que se seleccionan en hello **ámbito** panel o **resultados** panel. Hola **acciones** panel contiene Hola mismo comandos como hello **acción** menús que están disponibles para los elementos de hello **ámbito** panel y **resultados**panel. Para obtener una descripción de cada acción, vea la tabla Hola Hola **acción** sección de menú.

### <a name="examples"></a>Ejemplos
Hola toosee siguiente ejemplo de Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **programada**. Hola **acciones** panel muestra las acciones disponibles de Hola para hello **programada** nodo.

![Ejemplo de los trabajos programados del panel Acciones](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee más opciones, en hello **ámbito** panel, expanda hello **trabajos** nodo, haga clic en **programada**y, a continuación, haga clic en un trabajo programado en hello **resultados**panel. Hola **acciones** panel muestra las acciones disponibles de hello para el trabajo programado de hello, como se muestra en el siguiente ejemplo de Hola.

![Ejemplo de acciones de trabajo del panel Acciones](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Métodos abreviados y navegación mediante el teclado
Administrador de instantáneas StorSimple habilita las características de accesibilidad de Hola de sistema operativo de Windows de Hola y Hola Microsoft Management Console (MMC). También incluye algunas características de navegación de teclado y accesos directos específico toohello Administrador de instantáneas de StorSimple, como se describe en las secciones siguientes de Hola.

* [Teclas de navegación](#keyboard-navigation-keys) 
* [Teclas de método abreviado de la barra de menús](#menu-bar-shortcut-keys) 
* [Teclas de método abreviado del panel Ámbito](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Teclas de navegación
Hello tabla siguiente describen las claves de Hola que puede usar la interfaz de usuario de administrador de instantáneas StorSimple toonavigate Hola. 

| Tecla de navegación | Acción |
|:--- |:--- |
| Flecha abajo |Usar hello hacia abajo toomove teclas de flecha vertical toohello siguiente elemento en un menú o panel. |
| Escriba |Presione Hola ENTRAR clave toocomplete una acción y, a continuación, continuar toohello siguiente paso. Por ejemplo, puede presionar ENTRAR tooselect **siguiente**, **Aceptar**, o **crear**, y, a continuación, vaya toohello siguiente paso en un asistente. |
| Esc |Presione tooclose clave de hello Esc un menú o toocancel y cierre de una página. |
| F1 |Presione tooview clave de F1 de hello un tema de ayuda para la ventana actualmente activa Hola. |
| F5 |Presione Hola F5 clave toorefresh un nodo. |
| F6 |Presione F6 clave toomove de Hola de hello **ámbito** panel toohello **resultados** panel. |
| F10 |Presione la barra de menús de hello F10 toogo clave toohello. |
| Tecla de flecha izquierda |Usar hello dejado toomove teclas de flecha horizontal de una menú barra toohello anterior opción. Al mover toohello anterior aparece el menú del elemento en la barra de menú hello, los acción hello (o contextual) para el elemento anterior de Hola. |
| Tecla de flecha derecha |Utilizar Hola flecha derecha clave toomove horizontalmente en un menú barra opción toohello después. Al mover aparece toohello siguiente menú de elemento en la barra de menú hello, los acción hello (o contextual) para el nuevo elemento de Hola. |
| Tecla TAB |Use panel siguiente de hello ficha toomove clave toohello en hello consola o toohello siguiente selección o cuadro de texto en una página. |
| Tecla de flecha arriba |Usar hello una flecha clave toomove verticalmente toohello elemento anterior en un menú o panel. |

### <a name="menu-bar-shortcut-keys"></a>Teclas de método abreviado de la barra de menús
Hello tabla siguiente describen combinaciones de teclas de método abreviado de Hola de barra de menús de Hola. Después de presionar teclas de método abreviado de Hola y abre el menú de hello, puede usar teclas de método abreviado de menú (Hola teclas subrayadas en el menú de hello). Para obtener más información acerca de la barra de menús de hello, vaya demasiado[barra de menús](#menu-bar).

| Método abreviado | Resultado | Tecla de método abreviado de menú | Resultado |
|:--- |:--- |:--- |:--- |
| ALT + F |Se abre hello **archivo** menú. |N |Abre una nueva instancia de la consola. |
|  |O |Se abre hello **herramientas administrativas** página. | |
|  |S |Guarda la consola de administrador de instantáneas StorSimple Hola. | |
|  |Una  |Se abre hello **Guardar como** página. | |
|  |M |Se abre hello **agregar o quitar complemento** página. | |
|  |P |Se abre hello **opciones** página. | |
|  |H |Abre la Ayuda en pantalla. | |
| ALT + A |Se abre hello **acción** menú. |I |Opción de visualización de importación de hello activa y desactiva. |
|  |W |Abre una nueva consola de Administrador de instantáneas StorSimple. | |
|  |F |Actualiza la consola de administrador de instantáneas StorSimple Hola. | |
|  |L |Se abre hello **Exportar lista** página. | |
|  |H |Abre la Ayuda en pantalla. | |
| ALT + V |Se abre hello **vista** menú. |Una  |Se abre hello **agregar o quitar columnas** página. |
|  |U |Se abre hello **Personalizar vista** página. | |
| ALT + O |Se abre hello **favoritos** menú. |Una  |Se abre hello **agregar tooFavorites** página. |
|  |O |Se abre hello **Organizar favoritos** página. | |
| ALT + W |Se abre hello **ventana** menú. |N |Abre otra ventana de Administrador de instantáneas StorSimple. |
|  |C |Muestra todas las ventanas de consola abiertas en un estilo en cascada. | |
|  |T |Muestra todas las ventanas de consola abiertas en una cuadrícula. | |
|  |I |Organiza los iconos en una fila horizontal en la parte inferior de saludo de la pantalla. | |
| ALT + H |Se abre hello **ayuda** menú. |H |Abre la Ayuda en pantalla. |
|  |T |Abre la página web de Microsoft TechNet Tech Center de Hola. | |
|  |Una  |Se abre hello **sobre Microsoft Management Console** página. | |

### <a name="scope-pane-shortcut-keys"></a>Teclas de método abreviado del panel Ámbito
Hello siguientes tablas muestran contextual Hola combinaciones de teclas para cada nodo en hello **ámbito** panel. 

* [Teclas de método abreviado del nodo Dispositivos](#devices-node-shortcut-keys)
* [Teclas de método abreviado del nodo Volúmenes](#volumes-node-shortcut-keys)
* [Teclas de método abreviado del nodo Grupos de volúmenes](#volume-groups-node-shortcut-keys)
* [Teclas de método abreviado del nodo Directivas de copia de seguridad](#backup-policies-node-shortcut-keys)
* [Teclas de método abreviado del nodo Catálogo de copia de seguridad](#backup-catalog-node-shortcut-keys)
* [Teclas de método abreviado del nodo Trabajos](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Teclas de método abreviado del nodo Dispositivos
| Método abreviado de menú | Resultado |
|:--- |:--- |
| C |Se abre hello **configurar un dispositivo** página. |
| D |Actualiza la lista de Hola de dispositivos y los detalles del dispositivo. |
| V |Se abre hello **vista** menú. |
| W |Se abre una nueva consola de administrador de instantáneas StorSimple se centra en hello **detalles** nodo. |
| F |Actualiza la consola de administrador de instantáneas StorSimple Hola. |
| L |Se abre hello **Exportar lista** página. |
| H |Abre la Ayuda en pantalla. |

#### <a name="volumes-node-shortcut-keys"></a>Teclas de método abreviado del nodo Volúmenes
| Método abreviado de menú | Resultado |
|:--- |:--- |
| V |Lista de Hola de actualizaciones de volúmenes. |
| V (presione dos veces) |Se abre hello **vista** menú. |
| W |Se abre una nueva consola de administrador de instantáneas StorSimple se centra en hello **volúmenes** nodo. |
| F |Actualiza la consola de administrador de instantáneas StorSimple Hola. |
| L |Se abre hello **Exportar lista** página. |
| H |Abre la Ayuda en pantalla. |

#### <a name="volume-groups-node-shortcut-keys"></a>Teclas de método abreviado del nodo Grupos de volúmenes
| Método abreviado de menú | Resultado |
|:--- |:--- |
| G |Se abre hello **crear un grupo de volúmenes** página. |
| V |Se abre hello **vista** menú. |
| W |Se abre una nueva consola de administrador de instantáneas StorSimple se centra en hello **grupos de volúmenes** nodo. |
| F |Actualiza la consola de administrador de instantáneas StorSimple Hola. |
| L |Se abre hello **Exportar lista** página. |
| H |Abre la Ayuda en pantalla. |

#### <a name="backup-policies-node-shortcut-keys"></a>Teclas de método abreviado del nodo Directivas de copia de seguridad
| Método abreviado de menú | Resultado |
|:--- |:--- |
| B |Se abre hello **crear una directiva** página. |
| V |Se abre hello **vista** menú. |
| W |Se abre una nueva consola de administrador de instantáneas StorSimple se centra en hello **grupos de volúmenes** nodo. |
| F |Actualiza la consola de administrador de instantáneas StorSimple Hola. |
| L |Se abre Hola ** Exportar lista ** página. |
| H |Abre la Ayuda en pantalla. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Teclas de método abreviado del nodo Catálogo de copia de seguridad
| Método abreviado de menú | Resultado |
|:--- |:--- |
| W |Se abre una nueva consola de administrador de instantáneas StorSimple se centra en hello **grupos de volúmenes** nodo. |
| F |Actualiza la consola de administrador de instantáneas StorSimple Hola. |
| H |Abre la Ayuda en pantalla. |

#### <a name="jobs-node-shortcut-keys"></a>Teclas de método abreviado del nodo Trabajos
| Método abreviado de menú | Resultado |
|:--- |:--- |
| V |Se abre hello **vista** menú. |
| W |Se abre una nueva consola de administrador de instantáneas StorSimple se centra en hello **trabajos** nodo. |
| F |Actualiza la consola de administrador de instantáneas StorSimple Hola. |
| L |Se abre hello **Exportar lista** página. |
| H |Abre la Ayuda en pantalla |

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooconnect y administrar dispositivos](storsimple-snapshot-manager-manage-devices.md).

