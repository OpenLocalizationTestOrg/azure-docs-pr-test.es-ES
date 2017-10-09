---
title: "aaaUse un servidor local de SQL en aprendizaje automático de Azure | Documentos de Microsoft"
description: "Usar datos de un análisis de tooperform avanzada de base de datos de SQL Server local con aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Análisis avanzados con Aprendizaje automático de Azure con datos de una base de datos de SQL Server local

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

A menudo las empresas que funcionan con datos locales gustaría tootake aprovechar escala hello y la agilidad de la nube de Hola para su cargas de trabajo de aprendizaje automático. Pero que no deseen toodisrupt sus procesos empresariales actuales y los flujos de trabajo, mueva su local datos toohello en la nube. Ahora, Aprendizaje automático de Azure admite la lectura de los datos de una base de datos de SQL Server local, seguida del entrenamiento y la puntuación de un modelo con estos datos. Ya no tiene toomanually copiar y sincronización Hola datos entre la nube de Hola y el servidor local. En su lugar, Hola **importar datos** módulo en estudio de aprendizaje automático de Azure ahora puede leer directamente desde la base de datos de SQL Server local para el entrenamiento y la puntuación de trabajos.

Este artículo proporciona información general sobre cómo tooingress local datos de SQL server en aprendizaje automático de Azure. Se da por supuesto que conoce conceptos de Azure Machine Learning tales como áreas de trabajo, módulos, conjuntos de datos, experimentos, *etc.*

> [!NOTE]
> Esta característica no está disponible para las áreas de trabajo gratuitas. Para más información acerca de los niveles y los precios de Aprendizaje automático, consulte [Precios de Aprendizaje automático](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Instalar Microsoft Data Management Gateway Hola
tooaccess una base de datos de SQL Server local en aprendizaje automático de Azure, necesitará toodownload y Hola install Microsoft Data Management Gateway. Al configurar conexión de puerta de enlace de hello en estudio de aprendizaje automático, tendrá oportunidad de Hola para descargar e instalar la puerta de enlace de hello con hello **descarga y puerta de enlace de datos de registro** cuadro de diálogo se describe a continuación.

También puede instalar Hola Data Management Gateway antelación descargar y ejecutar el paquete de instalación MSI de Hola desde hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Elija la versión más reciente de hello, selección de 32 bits o 64 bits según corresponda para el equipo. Hola MSI también puede ser utilizado tooupgrade una existente Data Management Gateway toohello versión más reciente, con todas las opciones que se conservan.

puerta de enlace de Hello tiene Hola siguiendo los requisitos previos:

* versiones de sistema operativo de Windows Hello compatibles son Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2.
* Hola recomienda la configuración para la máquina de puerta de enlace de hello es al menos 2 GHz, 4 núcleos, 8GB de RAM y disco de 80GB.
* Si el equipo host de hello hiberna, puerta de enlace de hello no responderá toodata solicitudes. Por lo tanto, configurar un plan de alimentación adecuadas en el equipo de Hola antes de instalar la puerta de enlace de Hola. Si se utiliza una máquina de hello toohibernate configurado, instalación de puerta de enlace de hello muestra un mensaje.
* Como la actividad de copia se produce en una frecuencia determinada, Hola uso de recursos (CPU, memoria) en máquina hello también sigue Hola mismo patrón con las horas punta y tiempos de inactividad. Utilización de recursos también depende en gran medida cantidad Hola de datos que se mueven. Cuando haya varios trabajos de copia en curso, observará que el uso de los recursos aumenta durante las horas pico. Aunque técnicamente basta configuración mínima Hola mencionado anteriormente, puede querer toohave una configuración con más recursos de los requisitos mínimos de configuración de Hola según la carga específica para el movimiento de datos.

Considere Hola siguiente al configurar y usar una puerta de enlace de administración de datos:

* Solo puede instalar una instancia de Data Management Gateway en un solo equipo.
* Puede usar una sola puerta de enlace para varios orígenes de datos locales.
* Puede conectar varias puertas de enlace en distintos equipos toohello mismo origen de datos local.
* Una puerta de enlace se configura para una única área de trabajo al mismo tiempo. Actualmente, las puertas de enlace no se pueden compartir entre áreas de trabajo.
* Puede configurar varias puertas de enlace para una sola área de trabajo. Por ejemplo, puede que desee toouse una puerta de enlace que está conectado tooyour orígenes de datos de prueba durante el desarrollo y una puerta de enlace de producción cuando estés listo toooperationalize.
* puerta de enlace de Hello no es necesario toobe en hello mismo equipo como origen de datos de Hola. Pero mantenerse toohello más cerca de origen de datos reduce el tiempo de Hola Hola puerta de enlace tooconnect toohello origen de datos. Se recomienda que instale la puerta de enlace de hello en un equipo que es diferente de hello uno ese origen de datos de hosts Hola local para que hello puerta de enlace y origen de datos no entren en conflicto para los recursos.
* Si ya tiene una puerta de enlace instalada en el equipo que atiende los escenarios de Power BI o Data Factory de Azure, instale en otro equipo una independiente para Aprendizaje automático de Azure.

  > [!NOTE]
  > No se puede ejecutar la puerta de enlace de datos de administración y puerta de enlace de Power BI en hello mismo equipo.
  >
  >
* Debe toouse Hola Data Management Gateway para el aprendizaje automático de Azure incluso si utiliza Azure ExpressRoute de otros datos. Considere el origen de datos como uno de tipo local (que está detrás de un firewall), aunque utilice ExpressRoute. Usar la conectividad de tooestablish de Data Management Gateway Hola entre el aprendizaje automático y el origen de datos de Hola.

Puede encontrar información detallada sobre los requisitos previos de instalación, los pasos de instalación y sugerencias para solucionar problemas en el artículo hello [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Entrada de datos de la base de datos de SQL Server local en Aprendizaje automático de Azure
En este tutorial, instalará una instancia de Data Management Gateway en un área de trabajo de Aprendizaje automático de Azure, la configurará y después leerá datos de una base de datos de SQL Server local.

> [!TIP]
> Antes de comenzar, deshabilite el bloqueador de elementos emergentes del explorador para `studio.azureml.net`. Si usas Hola explorador Google Chrome, descargue e instale uno de hello varios complementos disponibles en Google Chrome WebStore [haga clic en una vez extensión de la aplicación](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Paso 1: Creación de una puerta de enlace
primer paso de Hello es toocreate y configurar hello tooaccess de puerta de enlace de la base de datos SQL local.

1. Inicie sesión demasiado[estudio de aprendizaje automático de Azure](https://studio.azureml.net/Home/) y área de trabajo de hello select que quiera toowork.
2. Haga clic en hello **configuración** hoja en hello izquierda y, a continuación, haga clic en hello **puertas de enlace de datos** ficha situada en la parte superior de Hola.
3. Haga clic en **nueva puerta de enlace de datos** en la parte inferior de Hola de pantalla de bienvenida.

    ![Nueva puerta de enlace de datos](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. Hola **nueva puerta de enlace de datos** cuadro de diálogo, escriba Hola **nombre de puerta de enlace** y, opcionalmente, agregue un **descripción**. Haga clic en la flecha Hola Hola inferior derecha toogo toohello siguiente paso de configuración de Hola.

    ![Especificación de la descripción y el nombre de la puerta de enlace](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. Hola descargar y registrar el cuadro de diálogo de la puerta de enlace de datos, copiar Portapapeles de toohello de clave de registro de puerta de enlace de Hola.

    ![Descarga y registro de la puerta de enlace de datos](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Si aún no ha descargado e instalado Hola Microsoft Data Management Gateway, a continuación, haga clic en **puerta de enlace de administración de datos de descarga**. Esta forma toothe Microsoft Download Center donde puede seleccionar la versión de la puerta de enlace de Hola necesita, descárguelo e instalarlo. Puede encontrar información detallada sobre los requisitos previos de instalación, los pasos de instalación y sugerencias para solucionar problemas en secciones de principio de Hola de artículo de hello [mover datos entre orígenes locales y en la nube con Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Después de instala la puerta de enlace de hello, Hola Administrador de configuración de Data Management Gateway se abrirá y Hola **puerta de enlace de registro** se muestra el cuadro de diálogo. Hola pegar **clave de registro de puerta de enlace** que copió toohello Portapapeles y haga clic en **registrar**.
8. Si ya tiene una puerta de enlace instalada, ejecute hello Administrador de configuración de Data Management Gateway. Haga clic en **cambiar la clave de**, pegue la **clave de registro de puerta de enlace** que copió toohello Portapapeles en el paso anterior de Hola y haga clic en **Aceptar**.
9. Una vez completada la instalación de hello, Hola **puerta de enlace de registro** se muestra el cuadro de diálogo para el Administrador de configuración de puerta de enlace de Microsoft Data Management. Pegue Hola clave de registro de puerta de enlace que ha copiado en el Portapapeles de hello en un paso anterior y haga clic en **registrar**.

    ![Registro de la puerta de enlace](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Hello configuración de puerta de enlace está completa cuando Hola siguientes valores se establece en hello **inicio** ficha en el Administrador de configuración de puerta de enlace de Microsoft Data Management:

    * **Nombre de puerta de enlace** y **nombre de instancia** se establecen toohello nombre de puerta de enlace de Hola.
    * **Registro** se establece demasiado**registrado**.
    * **Estado** se establece demasiado**iniciado**.
    * barra de estado de Hello en hello inferior muestra **conectado tooData servicio de nube de puerta de enlace de administración** junto con una marca de verificación verde.

      ![Administrador de Data Management Gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Estudio de aprendizaje automático de Azure también se actualiza al registro de hello es correcto.

    ![Registro de puerta de enlace correcto](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. Hola **descargar y registrar la puerta de enlace de datos** cuadro de diálogo, haga clic en el programa de instalación de marca de verificación toocomplete Hola. Hola **configuración** página muestra el estado de la puerta de enlace como "En línea". En el panel derecho de hello, encontrará estado y otra información útil.

    ![Configuración de puerta de enlace](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. En Administrador de configuración de Microsoft Data Management Gateway Hola cambie toohello **certificado** certificado de Hola de ficha especificado en esta pestaña está usado tooencrypt o descifrar credenciales de almacén de datos local de Hola que especifique en el portal de Hola. Este certificado es Hola de forma predeterminada. Microsoft recomienda cambiar este certificado propio tooyour copias de seguridad en el sistema de administración de certificados. Haga clic en **cambio** toouse su propio certificado en su lugar.

    ![Cambio del certificado de puerta de enlace](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (opcional) Si desea que tooenable el registro detallado con el fin de solucionar problemas relacionados con la puerta de enlace de hello, en Administrador de configuración de Microsoft Data Management Gateway Hola cambiar toothe **diagnósticos** ficha y compruebe hello **habilitar el registro detallado para fines de solución de problemas** opción. Hello información de registro puede encontrarse en hello Visor de eventos de Windows en hello **registros de aplicaciones y servicios**  - &gt; **Data Management Gateway** nodo. También puede usar hello **diagnósticos** ficha tootest Hola conexión tooan en origen de datos local con la puerta de enlace de Hola.

    ![Habilitación del registro detallado](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Con esto finaliza el proceso de instalación de puerta de enlace de hello en aprendizaje automático de Azure.
Se está ahora listo toouse los datos locales.

Puede crear y configurar varias puertas de enlace en Estudio para cada área de trabajo. Por ejemplo, puede tener una puerta de enlace que desea que los orígenes de datos de prueba de tooyour de tooconnect durante el desarrollo y una puerta de enlace diferentes de los orígenes de datos de producción. Aprendizaje automático de Azure ofrece la tooset flexibilidad de varias puertas de enlace según el entorno corporativo. Actualmente no se puede compartir una puerta de enlace entre áreas de trabajo y solamente se puede instalar una única puerta de enlace en un equipo. Para más información, consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Paso 2: Usar Hola puerta de enlace tooread datos de un origen de datos local
Después de configurar la puerta de enlace de hello, puede agregar un **importar datos** módulo para un experimento que escribe datos de saludo de base de datos de SQL Server de hello local.

1. En estudio de aprendizaje automático, seleccione hello **EXPERIMENTOS** , haga clic en **+ nuevo** en Hola esquina inferior izquierda y seleccione **en blanco de experimento** (o seleccione uno de varios ejemplos disponibles de experimentos).
2. Busque y arrastre hello **importar datos** toohello módulo experimentar lienzo.
3. Haga clic en **Guardar como** por debajo del lienzo de Hola. Especifique "Azure Machine Learning local Tutorial de SQL Server" para el nombre del experimento de hello, seleccione el área de trabajo y haga clic en hello **Aceptar** marca de verificación.

   ![Guardado de un experimento con un nuevo nombre](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Haga clic en hello **importar datos** tooselect de módulo, a continuación, en la **propiedades** toohello del panel derecho del lienzo de hello, seleccione "Base de datos local de SQL" en hello **origen de datos** lista desplegable.
5. Seleccione hello **puerta de enlace de datos** instalados y registrados. Puede configurar otra si selecciona "(add new Data Gateway…)" (Agregar nueva puerta de enlace de datos).

   ![Selección de la puerta de enlace de datos para el módulo de importación de datos](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Escriba Hola SQL **el nombre del servidor de base de datos** y **nombre de base de datos**, junto con hello SQL **consulta de base de datos** desea tooexecute.
7. Haga clic en **Enter values** (Escribir valores) de **User name and password** (Nombre de usuario y contraseña) y escriba sus credenciales de la base de datos. Puede usar la autenticación integrada de Windows o la autenticación de SQL Server según la configuración de SQL Server local.

   ![Especificación de las credenciales de la base de datos](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   mensaje de bienvenida de cambios de "valores requeridos" demasiado "valores establecidos" con una marca de verificación verde. Solo necesita las credenciales de hello tooenter una vez a menos que la información de la base de datos de Hola o una contraseña cambia. Aprendizaje automático de Azure utiliza certificados Hola que haya proporcionado al instalar las credenciales de hello puerta de enlace tooencrypt hello en la nube de Hola. Azure nunca almacena credenciales locales sin cifrado.

   ![Propiedades del módulo de importación de datos](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Haga clic en **ejecutar** experimento de hello toorun.

Una vez que finaliza la ejecución de experimento de hello, puede visualizar datos Hola importadas de base de datos de hello haciendo clic en el puerto de salida de hello de hello **importar datos** módulo y seleccionando **visualizar**.

Una vez que haya terminado de desarrollar el experimento, puede implementar el modelo y ponerlo en operación. Utilizando Hola servicio de ejecución por lotes, de hello local SQL Server base de datos configurado en hello **importar datos** módulo se leerán y se usa para puntuar. Aunque puede usar Hola servicio de respuesta de solicitud de puntuación de datos locales, Microsoft recomienda el uso de la [complemento de Excel](machine-learning-excel-add-in-for-web-services.md) en su lugar. Actualmente, escribir tooan local base de datos de SQL Server a través de **exportar datos** no es servicios web compatibles o en sus experimentos o publicada.
