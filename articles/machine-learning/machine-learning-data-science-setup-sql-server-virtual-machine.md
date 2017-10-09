---
title: "aaaSet una máquina virtual de SQL Server como un servidor de Bloc de notas de IPython | Documentos de Microsoft"
description: "Configurar una máquina virtual de ciencia de datos con SQL Server y IPython Server."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configuración de una máquina virtual de Azure SQL Server como servidor del Bloc de notas de IPython para realizar análisis avanzados
Este tema se muestra cómo tooprovision y configurar una toobe de máquina virtual de SQL Server utilizado como parte de un entorno de ciencia de datos en la nube. máquina virtual de Windows Hello se configura con compatibilidad con herramientas como Bloc de notas de IPython, Explorador de almacenamiento de Azure y AzCopy, así como otras utilidades que son útiles para los proyectos de ciencia de datos. Explorador de almacenamiento de Azure y AzCopy, por ejemplo, proporcionan a diversas formas rápidas de almacenamiento de blobs de tooupload datos tooAzure desde su equipo local o toodownload se tooyour el equipo local desde el almacenamiento de blobs.

la Galería de máquina virtual de Azure Hola incluye varias imágenes que contienen Microsoft SQL Server. Seleccione una imagen de máquina virtual de SQL Server que sea adecuada para sus necesidades de datos. Las imágenes recomendadas son:

* SQL Server 2012 SP2 Enterprise pequeño toomedium tamaños de datos
* SQL Server 2012 SP2 Enterprise optimizado para cargas de trabajo de almacén de datos para los tamaños de datos de gran tamaño toovery grandes
  
  > [!NOTE]
  > La imagen de SQL Server 2012 SP2 Enterprise **no incluye un disco de datos**. Se necesita especificar tooadd y adjuntar toostore de discos duros virtuales de uno o varios de los datos. Cuando se crea una máquina virtual de Azure, tiene un disco en la unidad de toohello C de sistema operativo asigna hello y una unidad de disco temporal asignado toohello D. No utilice datos de la unidad toostore Hola D. Como indica el nombre de hello, proporciona solo el almacenamiento temporal. No ofrece redundancia o copias de seguridad porque no reside en el almacenamiento de Azure.
  > 
  > 

## <a name="Provision"></a>Conectar toohello Portal clásico de Azure y aprovisionar una máquina virtual de SQL Server
1. Inicie sesión en toohello [portal de Azure clásico](http://manage.windowsazure.com/) con su cuenta.
   Si no tiene una cuenta de Azure, visite [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
2. En el portal de Azure clásico de hello, en la parte inferior izquierda de Hola de página web de hello, haga clic en **+ nuevo**, haga clic en **proceso**, haga clic en **máquina VIRTUAL**y, a continuación, haga clic en **FROM Galería de**.
3. En hello **crear una máquina Virtual** , seleccione una imagen de máquina virtual que contiene SQL Server según sus necesidades de datos y, a continuación, haga clic en hello flecha siguiente en la parte inferior derecha de la página de Hola. Para obtener información más actualizada de hello en hello admite imágenes de SQL Server en Azure, consulte [Introducción a SQL Server en máquinas virtuales Azure](http://go.microsoft.com/fwlink/p/?LinkId=294720) tema Hola [SQL Server en máquinas virtuales Azure](http://go.microsoft.com/fwlink/p/?LinkId=294719) conjunto de documentación.
   
   ![Selección de una máquina virtual de SQL Server][1]
4. En hello primera **configuración de máquina Virtual** , proporcione la siguiente información:
   
   * Especifique un **NOMBRE DE MÁQUINA VIRTUAL**.
   * Hola **nuevo nombre de usuario** cuadro, escriba el nombre de usuario único para la cuenta de administrador local de VM de Hola.
   * Hola **nueva contraseña** , escriba una contraseña segura. Para obtener más información, consulte [Contraseñas seguras](http://msdn.microsoft.com/library/ms161962.aspx).
   * Hola **Confirmar contraseña** cuadro, vuelva a escribir la contraseña de Hola.
   * Seleccione Hola adecuado **tamaño** de hello lista desplegable.
     
     > [!NOTE]
     > se especifica el tamaño de Hola de máquina virtual de Hola durante el aprovisionamiento: A2 es Hola menor tamaño recomendado para las cargas de trabajo de producción. El tamaño mínimo recomendado es A3 para una máquina virtual cuando se usa SQL Server Enterprise Edition. Seleccione A3 o un tamaño superior cuando use SQL Server Enterprise Edition. Seleccione A4 si usa SQL Server 2012 o 2014 Enterprise optimizado para imágenes de cargas de trabajo transaccionales.
     > Seleccione A7 si usa SQL Server 2012 o 2014 Enterprise optimizado para imágenes de cargas de trabajo de almacenamiento de datos. tamaño de Hello seleccionado limita el número de discos de datos que se puede configurar. Para obtener información más actualizada sobre tamaños de máquina virtual disponible y el número de Hola de discos de datos que puede asociar la máquina virtual de tooa, consulte [tamaños de máquina Virtual de Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Para obtener información sobre el precio, consulte [Precios de Máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Haga clic en la flecha siguiente de hello en toocontinue de hello inferior derecho.
   
   ![Configuración de una máquina virtual][2]
5. En hello segundo **configuración de máquina Virtual** página, configure los recursos de redes, almacenamiento y disponibilidad:
   
   * Hola **servicio de nube** cuadro, elija **crear un nuevo servicio de nube**.
   * Hola **nombre de DNS del servicio de nube** cuadro, proporcione Hola primera parte del nombre DNS que prefiera, de modo que complete un nombre en el formato **TESTNAME.cloudapp.net**
   * Hola **AFINIDAD región/grupo/red VIRTUAL** , seleccione una región donde se hospedará esta imagen virtual.
   * Hola **cuenta de almacenamiento**, seleccione una cuenta de almacenamiento existente o seleccione uno generado automáticamente.
   * Hola **conjunto de disponibilidad** cuadro, seleccione **(ninguno)**.
   * Lea y acepte Hola información sobre los precios.
6. Hola **EXTREMOS** sección, haga clic en la lista desplegable vacío de hello en **nombre**y seleccione **MSSQL** , a continuación, escriba el número de puerto de hello de la instancia de motor de base de datos (Hola**1433** para la instancia predeterminada de hello).
7. Su máquina virtual de SQL Server también puede actuar como servidor de Bloc de notas de IPython, que se configurará en un paso posterior.
   Agregar un nuevo toouse puerto de extremo toospecify hello para el servidor de Bloc de notas de IPython. Escriba un nombre en hello **nombre** columna, seleccione un número de puerto de su elección para el puerto público de Hola y 9999 para el puerto privado Hola.
   
   Haga clic en la flecha siguiente de hello en toocontinue de hello inferior derecho.
   
   ![Selección de puertos MSSQL y IPython][3]
8. Acepte el predeterminado de hello **agente de máquina virtual instalar** opción activada y haga clic en la marca de verificación de Hola Hola de hello inferior derecha de Hola Hola de toocomplete Asistente proceso de aprovisionamiento de máquinas virtuales.
   
   `![Opciones finales de máquina virtual][4]
9. Espere a que Azure prepare la máquina virtual. Esperar hello tooproceed de estado de máquina virtual a través de:
   
   * Inicio (aprovisionamiento)
   * Stopped
   * Inicio (aprovisionamiento)
   * Ejecución (aprovisionamiento)
   * En ejecución

## <a name="RemoteDesktop"></a>Máquina virtual Hola abierto a través de escritorio remoto y completar la instalación
1. Cuando finalice el aprovisionamiento, haga clic en el nombre de saludo de la página de panel de máquina virtual toogo toohello. En la parte inferior de Hola de página de hello, haga clic en **conectar**.
2. Elija tooopen Hola Mod archivo mediante el programa de escritorio remoto de Windows hello (`%windir%\system32\mstsc.exe`).
3. En hello **la seguridad de Windows** diálogo cuadro, proporcione la contraseña de hello para la cuenta de administrador local que especificó en un paso anterior.
   (Puede que tenga credenciales de hello tooverify de máquina virtual de Hola.)
4. Hello primera vez que inicie sesión en la máquina virtual de toothis, varios procesos necesite toocomplete, incluida la configuración de escritorio, actualizaciones de Windows y realización de tareas de configuración inicial de Windows hello (sysprep). Una vez que Sysprep de Windows finaliza, la configuración de SQL Server completa las tareas de configuración. Estas tareas pueden causar un retraso de unos minutos mientras se completan. `SELECT @@SERVERNAME`no se puede devolver el nombre correcto de hello hasta que finalice la instalación de SQL Server y SQL Server Management Studio no puede estar visible en la página de inicio de Hola.

Una vez que esté conectado toohello máquina con Escritorio remoto de Windows, Hola máquina virtual funciona prácticamente igual que cualquier otro equipo. Conectar toohello instancia de predeterminada de SQL Server con SQL Server Management Studio (que se ejecuta en la máquina virtual de hello) Hola forma normal.

## <a name="InstallIPython"></a>Instalación de Bloc de notas de IPython y otras herramientas de compatibilidad
tooconfigure su nueva tooserve de VM de SQL Server como un servidor de Bloc de notas de IPython y admitir adicionales de instalación de las herramientas tal AzCopy, Explorador de almacenamiento de Azure, paquetes de Python de ciencia de datos útiles y otros usuarios, se proporciona un script de personalización especial tooyou. tooinstall:

1. Menú contextual hello **inicio de Windows** icono y haga clic en **símbolo del sistema (Admin)**
2. Hola, siga los comandos de copiar y pegar en línea de comandos de Hola.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Cuando se le solicite, escriba una contraseña de su elección para hello servidor Bloc de notas de IPython.
4. script de personalización de Hello automatiza varios procedimientos posteriores a la instalación, que incluyen:
    * La instalación y configuración del servidor Bloc de notas de IPython.
    * Abrir puertos TCP en firewall de Windows hello para los extremos de Hola que creó anteriormente:
    * Para la conectividad remota de SQL Server
    * Para la conectividad remota del servidor de Bloc de notas de IPython
    * La obtención de Blocs de notas de IPython y scripts de SQL de ejemplo
    * La descarga e instalación de paquetes de Python de ciencia de datos útiles
    * La descarga e instalación de las herramientas de Azure como AzCopy y Explorador de almacenamiento de Azure   
    <br>
5. Se puede acceder y ejecutar el Bloc de notas de IPython desde cualquier explorador local o remoto mediante una dirección URL del formulario hello `https://<virtual_machine_DNS_name>:<port>`, donde puerto es el puerto público de hello IPython seleccionó al aprovisionar la máquina virtual de Hola.
6. Servidor de Bloc de notas de IPython se ejecuta como un servicio en segundo plano y se reiniciará automáticamente cuando se reinicia la máquina virtual de Hola.

## <a name="Optional"></a>Conectar discos de datos según sea necesario
Si la imagen VM no incluye discos de datos, es decir, los discos que no sea la unidad C (disco del sistema operativo) y la unidad D: (disco temporal), deberá tooadd uno o más datos discos toostore los datos. imagen de máquina virtual de Hola para SQL Server 2012 SP2 Enterprise optimizado para cargas de trabajo de almacén de datos viene preconfigurado con discos adicionales para los archivos de registro y datos de SQL Server.

> [!NOTE]
> No utilice datos de la unidad toostore Hola D. Como indica el nombre de hello, proporciona solo el almacenamiento temporal. No ofrece redundancia o copias de seguridad porque no reside en el almacenamiento de Azure.
> 
> 

discos de datos adicionales de tooattach, siga los pasos de hello descritos en [cómo tooAttach una máquina Virtual de Windows de disco de datos tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), que le guiará a través de:

1. Adjuntar discos vacíos toohello virtual machine aprovisionado en los pasos anteriores
2. Inicialización de nuevos discos de hello en la máquina virtual de Hola

## <a name="SSMS"></a>Conectar tooSQL Server Management Studio y habilitar la autenticación de modo mixto
Hola motor de base de datos de SQL Server no puede usar la autenticación de Windows sin el entorno de dominio. tooconnect toohello motor de base de datos desde otro equipo, configure SQL Server para la autenticación de modo mixto. La autenticación de modo mixto permite la autenticación de SQL Server y la autenticación de Windows. Se requiere el modo de autenticación de SQL datos de pedidos tooingest directamente desde las bases de datos de la máquina virtual de SQL Server en el [estudio de aprendizaje automático de Azure](https://studio.azureml.net) mediante el módulo de importación de datos de Hola.

1. Mientras la máquina virtual de toohello conectado mediante Escritorio remoto, use Windows hello **búsqueda** panel y escriba **SQL Server Management Studio** (SMSS). Haga clic en toostart Hola SQL Server Management Studio (SSMS). Puede que desee tooadd un tooSSMS de acceso directo en el escritorio para un uso futuro.
   
   ![Iniciar SSMS][5]
   
   primera vez que abra Management Studio debe crear el entorno de Management Studio de los usuarios de Hola Hola. Esta operación puede tardar unos minutos.
2. Cuando se abre, Management Studio presenta hello **conectar tooServer** cuadro de diálogo. Hola **nombre del servidor** cuadro, escriba un nombre Hola de máquina virtual de hello tooconnect toohello motor de base de datos con hello Explorador de objetos.
   (En lugar del nombre de la máquina virtual de hello también puede usar **(local)** o un punto único como hello **nombre del servidor**. Seleccione **autenticación de Windows**y dejar  ***su\_VM\_nombre*\\su\_local\_administrador**  en hello **nombre de usuario** cuadro. Haga clic en **Conectar**.
   
   ![Conectar tooServer][6]
   
   <br>
   
   > [!TIP]
   > Puede cambiar el modo de autenticación de SQL Server de hello mediante un cambio de clave de registro de Windows o con hello SQL Server Management Studio. modo de autenticación de toochange con cambio de clave del registro de hello, inicio una **nueva consulta** y ejecute la siguiente secuencia de comandos de hello:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    modo de autenticación de toochange Hola usando SQL Server management Studio:

1. En **Explorador de objetos de SQL Server Management Studio**, haga clic en el nombre de instancia de Hola de SQL Server (nombre de máquina virtual de hello) y, a continuación, haga clic en **propiedades**.
   
   ![Propiedades del servidor][7]
2. En hello **seguridad** página, en **autenticación de servidor**, seleccione **modo autenticación de Windows y SQL Server**y, a continuación, haga clic en **Aceptar** .
   
   ![Seleccionar el modo de autenticación][8]
3. Hola **SQL Server Management Studio** cuadro de diálogo, haga clic en **Aceptar** para confirmar el requisito de hello toorestart SQL Server.
4. En el **Explorador de objetos**, haga clic con el botón derecho en el servidor y, a continuación, haga clic en **Reiniciar**. (También se debe reiniciar Agente SQL Server si está en ejecución).
   
   ![Reiniciar][9]
5. Hola **SQL Server Management Studio** cuadro de diálogo, haga clic en **Sí** acepten que desea toorestart SQL Server.

## <a name="Logins"></a>Creación de inicios de sesión para la autenticación de SQL Server
tooconnect toohello motor de base de datos desde otro equipo, debe crear al menos un inicio de sesión de autenticación de SQL Server.  

Puede crear nuevos inicios de sesión de SQL Server mediante programación o utilizando Hola SQL Server Management Studio. toocreate un nuevo usuario de administrador del sistema con la autenticación de SQL mediante programación, iniciar un **nueva consulta** y ejecute la siguiente secuencia de comandos de Hola. Sustituya <new user name\> y <new password\> por el *nombre de usuario* y la *contraseña* que prefiera. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Ajustar la directiva de contraseña de hello según sea necesario (código de ejemplo de Hola desactiva la expiración de contraseña y la comprobación de la directiva). Para ver más información acerca de los inicios de sesión de SQL Server, consulte [Crear un inicio de sesión](http://msdn.microsoft.com/library/aa337562.aspx).  

Hola a toocreate nuevo SQL Server los inicios de sesión mediante SQL Server Management Studio:

1. En **Explorador de objetos de SQL Server Management Studio**, expanda la carpeta Hola de instancia del servidor hello en el que desea que el nuevo inicio de sesión de toocreate Hola.
2. Menú contextual hello **seguridad** carpeta, seleccione demasiado**nuevo**y seleccione **inicio de sesión...** .
   
   ![Nuevo inicio de sesión][10]
3. Hola **inicio de sesión - nuevo** cuadro de diálogo de hello **General** página, escriba el nombre de Hola de nuevo usuario de Hola Hola **nombre de inicio de sesión** cuadro.
4. Seleccione **Autenticación de SQL Server**.
5. Hola **contraseña** cuadro, escriba una contraseña para hello nuevo usuario. Vuelva a escribir la contraseña en hello **Confirmar contraseña** cuadro.
6. Opciones de directiva de contraseña de tooenforce de complejidad y exigencia, seleccione **exigir directivas de contraseñas** (recomendado). Esta es una opción predeterminada cuando se selecciona la autenticación de SQL Server.
7. Opciones de directiva de contraseña tooenforce para la expiración, seleccione **exigir expiración de contraseña** (recomendado). Exigir directivas de contraseñas debe estar seleccionado tooenable esta casilla de verificación. Esta es una opción predeterminada cuando se selecciona la autenticación de SQL Server.
8. tooforce Hola usuario toocreate se utiliza una contraseña nueva después de hello es la primera vez el inicio de sesión, seleccione **usuario debe cambiar la contraseña en el siguiente inicio de sesión** (recomendado si este inicio de sesión es para un usuario toouse else. Si el inicio de sesión de hello es para uso propio, no seleccione esta opción.) Exigir expiración de contraseña debe ser tooenable seleccionada esta casilla de verificación. Esta es una opción predeterminada cuando se selecciona la autenticación de SQL Server.
9. De hello **base de datos predeterminada** , seleccione una base de datos predeterminada para el inicio de sesión de Hola. **maestro** es Hola predeterminado para esta opción. Si aún no ha creado una base de datos de usuario, deje este conjunto demasiado**principal**.
10. Hola **idioma predeterminado** lista, deje **predeterminado** como valor de Hola.
    
    ![Propiedades de inicio de sesión][11]
11. Si se trata de hello primer inicio de sesión que está creando, puede que desee designar este inicio de sesión como administrador de SQL Server. En ese caso, en la página **Roles de servidor**, active **sysadmin**.
    
    > [!IMPORTANT]
    > Los miembros del rol fijo de servidor sysadmin hello tienen control completo de hello motor de base de datos. Deberá restringir cuidadosamente la suscripción en este rol por motivos de seguridad.
    > 
    > 
    
    ![sysadmin][12]
12. Haga clic en Aceptar.

## <a name="DNS"></a>Determinar el nombre DNS de Hola de máquina virtual de Hola
tooconnect toohello motor de base de datos de SQL Server desde otro equipo, debe conocer Hola sistema de nombres de dominio (DNS) nombre de máquina virtual de Hola.

(Esto es nombre Hola Hola usa internet tooidentify virtual Hola máquina. Puede usar la dirección IP de hello, pero puede cambiar la dirección IP de hello cuando Azure mueve recursos por redundancia o mantenimiento. nombre DNS de Hello será estable porque puede ser redirigido tooa nueva dirección IP.)

1. En el Portal de Azure clásico de hello (o del paso anterior de hello), seleccione **máquinas virtuales**.
2. En hello **instancias de máquina VIRTUAL** página Hola **nombre DNS** precedida de la columna, busque y copiar nombre DNS de hello para la máquina virtual de Hola que aparece **http://**. (interfaz de usuario de hello no puede mostrar el nombre completo de hello, pero puede haga doble clic en él y seleccione Copiar.)

## <a name="cde"></a>Conectar toohello motor de base de datos desde otro equipo
1. En un equipo conectado toohello internet, abra SQL Server Management Studio.
2. Hola **conectar tooServer** o **conectar tooDatabase motor** cuadro de diálogo hello **nombre del servidor** cuadro, escriba el nombre DNS de saludo de la máquina virtual (determinada en hello tarea anterior) y un número de puerto de extremo público en formato de Hola de *DNSName, portnumber* como **tutorialtestVM.cloudapp.net,57500**.
3. Hola **autenticación** cuadro, seleccione **autenticación de SQL Server**.
4. Hola **inicio de sesión** cuadro, escriba un nombre Hola de un inicio de sesión que creó en una tarea anterior.
5. Hola **contraseña** cuadro, escriba la contraseña de inicio de sesión de Hola que cree en una tarea anterior Hola.
6. Haga clic en **Conectar**.

## <a name="amlconnect"></a>Conectar toohello motor de base de datos de aprendizaje automático de Azure
En las fases posteriores de hello proceso de ciencia de datos de equipo, deberá utilizar hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net) toobuild e implementar modelos de aprendizaje automático. tooingest datos de las bases de datos de la máquina virtual de SQL Server directamente en aprendizaje automático de Azure para el entrenamiento o de puntuación, usar hello **importar datos** módulo en una nueva [estudio de aprendizaje automático de Azure](https://studio.azureml.net) experimentar. Este tema se trata con más detalle a través de hello vínculos de guía de procesos de ciencia de datos de equipo. Para obtener una introducción, consulte [¿Qué es Estudio de aprendizaje automático de Azure?](machine-learning-what-is-ml-studio.md)

1. Hola **propiedades** panel de hello [módulo importar datos](https://msdn.microsoft.com/library/azure/dn905997.aspx), seleccione **base de datos de SQL Azure** de hello **origen de datos** lista desplegable.
2. Hola **el nombre del servidor de base de datos** texto cuadro, escriba`tcp:<DNS name of your virtual machine>,1433`
3. Escriba el nombre de usuario SQL de Hola Hola **nombre de cuenta de usuario de servidor** cuadro de texto.
4. Escriba la contraseña del usuario de sql de hello en hello **contraseña de cuenta de usuario de servidor** cuadro de texto.
   
   ![Importar datos de Azure Machine Learning][13]

## <a name="shutdown"></a>Apagado y desasignación de la máquina virtual cuando no esté en uso
Las máquinas virtuales de Azure tienen unas tarifas del tipo **pague solo por lo que use**. tooensure que no están siendo factura cuando no se utiliza la máquina virtual, tiene toobe en hello **detenido (desasignado)** estado.

> [!NOTE]
> Apagando la máquina virtual de Hola desde dentro de (mediante opciones de energía de Windows), hello VM se detiene pero sigue siendo asignado. tooensure que no se le facturan, siempre se detendrá máquinas virtuales de hello [Portal clásico de Azure](http://manage.windowsazure.com/). También puede detener Hola VM a través de Powershell mediante una llamada a ShutdownRoleOperation con "PostShutdownAction" igual demasiado "StoppedDeallocated".
> 
> 

tooshutdown y cancelar la asignación de máquina virtual de hello:

1. Inicie sesión en toohello [Portal clásico de Azure](http://manage.windowsazure.com/) con su cuenta.  
2. Seleccione **máquinas virtuales** de barra de navegación izquierda de Hola.
3. En la lista de Hola de máquinas virtuales, haga clic en nombre de hello de la máquina virtual, a continuación, vaya toohello **panel** página.
4. En la parte inferior de Hola de página de hello, haga clic en **apagado**.

![Apagado de máquina virtual][15]

se cancela la asignación de máquina virtual de Hello pero no se eliminarán. Puede reiniciar la máquina virtual en cualquier momento desde Hola Portal clásico de Azure.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>La máquina virtual de Azure SQL Server está listo toouse: ¿qué es el siguiente?
La máquina virtual está ahora listo toouse en los ejercicios de ciencia de datos. máquina virtual de Hello también está listo para su uso como un servidor de Bloc de notas de IPython de exploración de Hola y el procesamiento de datos y otras tareas junto con hello proceso de ciencia de datos de equipo (TDSP) y el aprendizaje automático de Azure.

pasos siguientes en el proceso de ciencia de datos Hola Hola se asignan una Hola [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) y pueden incluir los pasos que se mueven datos en HDInsight, proceso y ejemplo allí como preparación para el aprendizaje a partir de los datos de hello con el equipo de Azure El aprendizaje.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

