---
title: "Planificador de implementación de Site Recovery aaaAzure de VMware a Azure | Documentos de Microsoft"
description: "Se trata de una guía de usuario del programador de implementación de hello Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery Deployment Planner
Este artículo es manual de usuario de hello planificador de implementación de recuperación de sitio de Azure para las implementaciones de producción de VMware en Azure.

## <a name="overview"></a>Información general

Antes de empezar a proteger las máquinas virtuales (VM) de VMware mediante el uso de Site Recovery, asignar suficiente ancho de banda, según su tasa de cambio de datos diaria, toomeet su objetivo de punto de recuperación deseado (RPO). Ser seguro toodeploy Hola derecho número de servidores de configuración y proceso servidores locales.

También necesitará tipo correcto de toocreate Hola y el número de cuentas de almacenamiento de Azure de destino. Cree cuentas de almacenamiento Estándar o Premium, para lo que debe tener en cuenta el crecimiento en los servidores de producción de origen debido al aumento del uso con el paso del tiempo. Elegir tipo de almacenamiento de Hola por máquina virtual, basándose en las características de carga de trabajo (por ejemplo, operaciones de E/S de lectura/escritura por segundo [IOPS] o renovación de datos) y límites de Site Recovery.

Hola Site Recovery implementación planner versión preliminar pública es una herramienta de línea de comandos que esté disponible solo para el escenario de VMware a Azure Hola. Puede generar perfiles de las máquinas virtuales de VMware con este ancho de banda de la herramienta (con ningún impacto en la producción sea) toounderstand hello y los requisitos de almacenamiento de Azure para la replicación correcta y probar la conmutación por error de forma remota. Puede ejecutar la herramienta de Hola sin necesidad de instalar los componentes Site Recovery en local. Sin embargo, tooget preciso conseguir resultados del rendimiento, recomendamos que ejecute planificador de hello en un servidor de Windows que cumple los requisitos de hello mínimos Hola recuperación del sitio del servidor de configuración que finalmente deberá toodeploy como uno de los primeros pasos de Hola en la implementación de producción.

herramienta de Hello proporciona Hola detalles siguientes:

**Evaluación de compatibilidad**

* Evaluación de la idoneidad de la máquina virtual en función del número de discos, el tamaño de estos, las IOPS, la actividad de datos y el tipo de arranque (EFI/BIOS)
* Hola de ancho de banda de red estimado necesario para la replicación de datos

**Necesidad de ancho de banda de red frente a evaluación de RPO**

* Hola de ancho de banda de red estimado necesario para la replicación de datos
* rendimiento de Hola que obtienen de Site Recovery tooAzure local
* número de Hola de toobatch de máquinas virtuales, en función de hello estimado replicación inicial de toocomplete de ancho de banda en un período determinado de tiempo

**Requisitos de infraestructura de Azure**

* requisito de tipo (cuenta de almacenamiento standard o premium) de almacenamiento de Hola para cada máquina virtual
* número total de Hola de toobe de cuentas de almacenamiento estándar y premium configurado para replicación
* Sugerencias de nomenclatura de las cuentas de almacenamiento, según la guía de Azure Storage
* selección de ubicación de cuenta de almacenamiento de Hola para todas las máquinas virtuales
* configurar el número de Hola de núcleos Azure toobe antes de la conmutación por error o conmutación por error en la suscripción de Hola
* Hola tamaño recomendado de máquina virtual de Azure para cada máquina virtual local

**Requisitos de la infraestructura local**
* número de servidores de configuración necesarios de Hola y toobe de servidores de proceso implementa local

>[!IMPORTANT]
>
>Dado que el uso es probable que tooincrease con el tiempo, todos Hola herramienta anterior se realizan cálculos suponiendo un factor de crecimiento del 30 por ciento en las características de carga de trabajo y el uso de un valor del percentil 95 del programa Hola a todos las métricas de generación de perfiles (lectura/escritura de e/s por segundo, renovación de modo que hacia delante). Ambos elementos (el cálculo del percentil y el factor de crecimiento) se pueden configurar. toolearn más información acerca del factor de crecimiento, vea la sección de "Consideraciones de factor de crecimiento" de Hola. toolearn más información sobre el valor de percentil, vea la sección de "Valor de percentil utilizado para el cálculo de Hola" de Hola.
>

## <a name="requirements"></a>Requisitos
herramienta de Hello tiene dos fases principales: generación de perfiles y generación de informes. También hay un tercera opción toocalculate exclusivamente al rendimiento. requisitos de Hola para servidor hello desde qué Hola se inicia la medición del rendimiento y generación de perfiles se presentan en hello en la tabla siguiente:

| Requisito del servidor | Descripción|
|---|---|
|Generación de perfiles y medición de rendimiento| <ul><li>Sistema operativo: Microsoft Windows Server 2012 R2<br>(al menos lo ideal es que la búsqueda de coincidencias Hola [cambiar el tamaño de las recomendaciones para el servidor de configuración de hello](https://aka.ms/asr-v2a-on-prem-components))</li><li>Configuración del equipo: 8 vCPU, 16 GB de RAM y 300 GB de HDD</li><li>[Microsoft .NET 4.5 Framework](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Microsoft Visual C++ Redistributable para Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>TooAzure de acceso a Internet desde este servidor</li><li>Cuenta de almacenamiento de Azure</li><li>Acceso de administrador en el servidor de Hola</li><li>Mínimo de 100 GB de espacio libre en disco (asumiendo 1000 máquinas virtuales con un promedio de tres discos cada una, con perfil para 30 días)</li><li>Debe establecerse la configuración del nivel de VMware vCenter estadísticas too2 o alto nivel</li><li>Permitir el puerto 443: ASR Deployment Planner utiliza este puerto tooconnect toovCenter server/ESXi host</ul></ul>|
| Generación de informes | Un PC con Windows o Windows Server con Microsoft Excel 2013, o cualquier versión posterior |
| Permisos de usuario | Permiso de solo lectura para cuenta de usuario de Hola que ha utilizado el host de tooaccess Hola VMware vCenter server/VMware vSphere ESXi durante la generación de perfiles |

> [!NOTE]
>
>herramienta de Hello puede generar perfiles solo las máquinas virtuales con discos VMDK y RDM. No se pueden generar perfiles de máquinas virtuales con discos iSCSI o NFS. Recuperación de sitio admite iSCSI y discos NFS para servidores de VMware pero, dado que planificador de implementación de hello no está dentro de invitado de Hola y lo perfiles únicamente mediante los contadores de rendimiento de vCenter, herramienta de hello no tiene visibilidad en estos tipos de disco.
>

## <a name="download-and-extract-hello-public-preview"></a>Descargue y extraiga la versión preliminar pública de Hola
1. Descargar Hola la versión más reciente de hello [versión preliminar pública de Site Recovery implementación planner](https://aka.ms/asr-deployment-planner).  
herramienta de Hola se empaqueta en una carpeta zip. versión actual de Hola de herramienta Hola admite solo el escenario de VMware a Azure Hola.

2. Copia Hola .zip carpeta toohello Windows server del que desea que la herramienta de hello toorun.  
Puede ejecutar herramienta Hola desde Windows Server 2012 R2 si el servidor de hello tiene acceso tooconnect toohello vCenter server/vSphere ESXi host de red que contiene toobe de máquinas virtuales de hello perfilar. Sin embargo, recomendamos que ejecute la herramienta de hello en un servidor cuya configuración de hardware cumple hello [directriz de ajuste de tamaño del servidor de configuración](https://aka.ms/asr-v2a-on-prem-components). Si ya ha implementado componentes de Site Recovery en local, ejecute la herramienta de Hola desde el servidor de configuración de Hola.

 Recomendamos que posea Hola misma configuración de hardware como un servidor de configuración de hello (que tiene un servidor de proceso incorporado) en servidor hello donde se ejecuta la herramienta de Hola. Esta configuración garantiza un ese rendimiento Hola lograda que Hola herramienta informes coincidencias Hola real rendimiento que puede lograr la recuperación del sitio durante la replicación. cálculo del rendimiento Hola depende de ancho de banda de red disponible en el servidor de Hola y configuración de hardware (CPU, almacenamiento etc.) del servidor de Hola. Si ejecuta la herramienta Hola de cualquier otro servidor, rendimiento de Hola se calcula a partir de ese tooMicrosoft servidor Azure. Además, porque la configuración de hardware de Hola de servidor hello puede diferir de saludo servidor de configuración, rendimiento de hello lograda que Hola herramienta informes puede ser imprecisa.

3. Extraiga la carpeta de .zip Hola.  
carpeta de Hello contiene varios archivos y subcarpetas. archivo ejecutable hello es ASRDeploymentPlanner.exe en la carpeta principal de Hola.

    Ejemplo:  
    Copie tooE de archivo .zip de hello: \ unidad y extráigalo.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Capacidades
Puede ejecutar la herramienta de línea de comandos de hello (ASRDeploymentPlanner.exe) en cualquiera de hello después de tres modos:

1. Generación de perfiles  
2. Generación de informes
3. Obtención de rendimiento

Herramienta de hello en primer lugar, la ejecución de generación de perfiles de renovación de datos de máquina virtual de modo toogather e IOPS. A continuación, ejecute informes de hello herramienta toogenerate Hola requisitos de ancho de banda y almacenamiento de la red del hello toofind.

## <a name="profiling"></a>Generación de perfiles
En el modo de generación de perfiles, herramienta de planeación de implementación de hello conecta toohello vCenter server/vSphere ESXi datos de rendimiento de toocollect de host de VM de Hola.

* Generación de perfiles no afecta a rendimiento Hola de producción de hello las máquinas virtuales, porque no hay ninguna conexión directa se realiza toothem. Recopila todos los datos de rendimiento del host de hello vCenter server/vSphere ESXi.
* tooensure que hay un efecto insignificante en el servidor de Hola a causa de generación de perfiles, Hola herramienta consultas Hola vCenter server/vSphere host ESXi cada 15 minutos. Este intervalo de consulta no poner en peligro la precisión de generación de perfiles, porque la herramienta de hello almacena los datos del contador de rendimiento de cada minuto.

### <a name="create-a-list-of-vms-tooprofile"></a>Crear una lista de las máquinas virtuales tooprofile
En primer lugar, necesita una lista de toobe de las máquinas virtuales de hello perfilar. Puede obtener todos los nombres de Hola de máquinas virtuales en un host de vCenter server/vSphere ESXi mediante comandos de hello VMware vSphere PowerCLI Hola siguiendo el procedimiento. Como alternativa, puede ver una lista en un archivo hello descriptivo los nombres o direcciones IP de Hola máquinas virtuales que desea tooprofile manualmente.

1. Inicie sesión en toohello VM ese vSphere de VMware PowerCLI se instala en.
2. Abra la consola de hello VMware vSphere PowerCLI.
3. Asegúrese de que está habilitada la directiva de ejecución de Hola para script de Hola. Si está deshabilitada, iniciar la consola de hello VMware vSphere PowerCLI en modo de administrador y, a continuación, habilitarlo al ejecutar el siguiente comando de hello:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. Es posible necesidad de opción toorun Hola siguiente comando si VIServer Connect no se reconoce como nombre de Hola de cmdlet.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget todos los nombres de Hola de máquinas virtuales en un servidor de vCenter/vSphere ESXi hospedan y almacenan la lista de hello en un archivo .txt, dos comandos de ejecución Hola enumerados aquí.
Reemplace &lsaquo;server name&rsaquo; (nombre del servidor), &lsaquo;user name&rsaquo; (nombre de usuario), &lsaquo;password&rsaquo; (contraseña), &lsaquo;outputfile.txt&rsaquo;; (archivo de salida.txt) por sus entradas.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Abra el archivo de salida de hello en el Bloc de notas y, a continuación, copie nombres Hola de todas las máquinas virtuales que desee tooprofile tooanother archivo (por ejemplo, ProfileVMList.txt), un nombre de máquina virtual por línea. Este archivo se usa como entrada toohello *VMListFile -* parámetro de la herramienta de línea de comandos Hola.

    ![Lista de nombres de máquina virtual en planes de implementación de Hola](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Inicio de la generación de perfiles
Una vez haya lista Hola de toobe de las máquinas virtuales que se generan perfiles, se puede ejecutar la herramienta de hello en el modo de generación de perfiles. Aquí está lista Hola de parámetros obligatorios y opcionales de hello herramienta toorun en modo de generación de perfiles.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Nombre de parámetro | Descripción |
|---|---|
| -Operation | Inicio de la generación de perfiles |
| -Server | nombre de dominio completo de Hola o dirección IP del host del servidor/vSphere ESXi de hello vCenter cuyas máquinas virtuales son toobe perfilada.|
| -User | Hola usuario nombre tooconnect toohello vCenter server/vSphere host ESXi. usuario de Hello necesita acceso de solo lectura toohave, como mínimo.|
| -VMListFile | archivo de Hola que contiene la lista de Hola de toobe de las máquinas virtuales que se generan perfiles. ruta de acceso de archivo Hello puede ser absoluta o relativa. archivo Hello debe contener una máquina virtual nombre o dirección IP por línea. Nombre de la máquina virtual especificada en el archivo hello debe ser Hola igual que el nombre de la máquina virtual de hello en el host de hello vCenter server/vSphere ESXi.<br>Por ejemplo, el archivo hello VMList.txt contiene Hola después de las máquinas virtuales:<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | Hola número de días durante la generación de perfiles está toobe la ejecución. Le recomendamos que ejecute durante más de 15 días tooensure que Hola patrón de carga de trabajo en su entorno a través de hello especificado período se observa y utiliza tooprovide una recomendación precisa de generación de perfiles. |
| -Directory | Convención de nomenclatura universal (UNC) de hello (opcional) o toostore de ruta de acceso de directorio local generados durante la generación de perfiles de datos de generación de perfiles. Si no se proporciona un nombre de directorio, directory Hola denominado 'ProfiledData' en la ruta de acceso actual de Hola se utilizará como directorio predeterminado de Hola. |
| -Password | Hola (opcional) contraseña toouse tooconnect toohello vCenter server/vSphere host ESXi. Si no especifica uno ahora, se le pedirá que cuando se ejecuta el comando Hola.|
| -StorageAccountName | Nombre de la cuenta de almacenamiento de hello (opcional) que es el rendimiento de hello toofind usado factible para replicación de datos de tooAzure en local. Hola herramienta cargas prueba datos toothis cuenta toocalculate rendimiento del almacenamiento.|
| -StorageAccountKey | Clave de cuenta de almacenamiento de hello (opcional) que ha utilizado la cuenta de almacenamiento de tooaccess Hola. Vaya toohello portal de Azure > cuentas de almacenamiento ><*nombre de la cuenta de almacenamiento*>> Configuración > claves de acceso > Key1 (o clave de acceso principal para la cuenta de almacenamiento clásico). |
| -Environment | (Opcional) Se trata del entorno de la cuenta de Azure Storage de destino. Puede ser uno de estos tres valores: AzureCloud, AzureUSGovernment y AzureChinaCloud. El valor predeterminado es AzureCloud. Use el parámetro de hello cuando la región de Azure de destino es nubes Azure gobierno de Estados Unidos o en Azure China. |


Se recomienda que se generan perfiles de las máquinas virtuales para al menos 15 días de too30. Durante el período de generación de perfiles de hello, ASRDeploymentPlanner.exe sigue ejecutándose. herramienta de Hello toma la entrada en tiempo de generación de perfiles en días. Si desea tooprofile durante algunas horas o minutos para una prueba rápida de herramienta de hello, en vista previa pública de hello, necesitará tooconvert tiempo de hello en medida equivalente de Hola de días. Por ejemplo, tooprofile durante 30 minutos, la entrada de hello debe ser 30/(60*24) = 0.021 días. Hola mínimo permitido de tiempo de generación de perfiles es de 30 minutos.

Durante la generación de perfiles, también puede pasar un nombre de cuenta de almacenamiento y el rendimiento de hello toofind clave que puede lograr Site Recovery en tiempo de Hola de replicación desde el servidor de configuración de Hola o tooAzure de servidor de proceso. Si no se pasan clave y el nombre de cuenta de almacenamiento de Hola durante la generación de perfiles, herramienta de hello no calcula capacidad de proceso.

Puede ejecutar varias instancias de la herramienta de Hola para diversos conjuntos de máquinas virtuales. Asegúrese de que no se repiten nombres de máquina virtual de hello en cualquiera de hello conjuntos de generación de perfiles. Por ejemplo, si ha Perfilar diez máquinas virtuales (VM1 a través de VM10) y después de algunos días desea tooprofile otro cinco VM (VM11 a través de VM15), puede ejecutar herramienta Hola desde otra consola de línea de comandos para el segundo conjunto de máquinas virtuales de hello (VM11 a través de VM15). Asegúrese de que segundo conjunto de máquinas virtuales de hello no tiene ningún nombre de máquina virtual desde la primera instancia de generación de perfiles Hola o utilizar un directorio de salida diferente para hello segunda ejecución. Si dos instancias de la herramienta de Hola se usan para la generación de perfiles de hello misma máquinas virtuales y use Hola mismo directorio de salida, informe de hello generado será incorrecta.

Configuraciones de máquina virtual captura una vez al principio de Hola de hello operación de generación de perfiles y se almacenan en un archivo denominado VMDetailList.xml. Esta información se usa cuando se genera el informe de Hola. No se captura ningún cambio en la configuración de máquina virtual (por ejemplo, un mayor número de núcleos, discos o NIC) de hello principio toohello final de generación de perfiles. Si ha cambiado una configuración de VM perfiles durante el transcurso de Hola de generación de perfiles, en la versión preliminar pública de hello, mostramos detalles más recientes de VM de hello solución tooget al generar el informe de hello:

* Hacer copia de seguridad VMdetailList.xml y eliminar archivo hello desde su ubicación actual.
* Pasar - usuario ni - Password argumentos en tiempo de presentación de la generación de informes.

Hola comando de generación de perfiles genera varios archivos en el directorio de generación de perfiles de Hola. No elimine ninguno de los archivos de hello, porque al hacerlo por lo que afecta a la generación de informes.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Ejemplo 1: Máquinas virtuales de perfil para 30 días y el rendimiento de Hola de búsqueda de tooAzure local
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Ejemplo 2: Generar perfiles de máquinas virtuales durante 15 días

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Ejemplo 3: Máquinas virtuales de perfil durante una hora para una prueba rápida de herramienta Hola
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Si servidor de hello esa herramienta Hola está ejecutando en se reinicia o se ha bloqueado, o si cierra Hola herramienta mediante el uso de Ctrl + C, datos de hello perfilada se conserva. Sin embargo, hay una posibilidad de hello falta últimos 15 minutos de datos del perfil. En ese caso, vuelva a ejecutar la herramienta de hello en el modo de generación de perfiles una vez reiniciado el servidor de Hola.
>* Cuando se pasan Hola nombre de cuenta de almacenamiento y la clave, rendimiento de hello herramienta medidas hello en el último paso de Hola de generación de perfiles. Si se cierra la herramienta de hello antes de que finalice la generación de perfiles, rendimiento de hello no se calcula. Hola de rendimiento de hello toofind antes de generar informes, puede ejecutar hello GetThroughput operación desde la consola de línea de comandos de Hola. En caso contrario, informe de hello generado no contendrá información de rendimiento de Hola.


## <a name="generate-a-report"></a>Generación de un informe
herramienta de Hello genera un archivo de Microsoft Excel habilitado para macros (archivo XLSM) como salida del informe hello, que resume todas las recomendaciones de implementación de Hola. informe de Hola se denomina DeploymentPlannerReport_ <*identificador numérico único*> colocados en hello y .xlsm especifican el directorio.

Una vez completada la generación de perfiles, puede ejecutar la herramienta hello en el modo de generación de informes. Hello en la tabla siguiente contiene una lista de toorun de parámetros de herramienta obligatorios y opcionales en el modo de generación de informes.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Nombre de parámetro | Descripción |
|-|-|
| -Operation | GenerateReport |
| -Server |  servidor de vCenter/vSphere Hola completo nombre de dominio o dirección IP (use Hola mismo nombre o dirección IP que utiliza en tiempo de Hola de generación de perfiles) donde hello Perfilar cuyo informe es toobe generado de las máquinas virtuales se encuentran. Tenga en cuenta que si usa un servidor vCenter al tiempo de Hola de generación de perfiles, no puede usar un servidor de vSphere para la generación de informes y viceversa.|
| -VMListFile | archivo de Hola que contiene la lista de Hola de máquinas virtuales para que informe de Hola es toobe generado para. ruta de acceso de archivo Hello puede ser absoluta o relativa. Hola archivo debe contener un nombre de máquina virtual o la dirección IP por línea. nombres de Hello las VM que se especifican en el archivo hello debe ser Hola igual que los nombres de las VM hello en host ESXi de hello vCenter server/vSphere y coincidencia que se utilizó durante la generación de perfiles.|
| -Directory | (Opcional) Hola UNC o ruta de acceso del directorio local donde hello Perfilar datos (archivos generados durante la generación de perfiles) se almacena. Estos datos son necesarios para generar informes de Hola. Si no se especifica ningún nombre, se usará el directorio 'ProfiledData'. |
| -GoalToCompleteIR | Hola (opcional) número de horas en qué Hola la replicación inicial de hello Perfilar máquinas virtuales debe toobe completado. informe de Hello genera proporciona Hola número de máquinas virtuales para los que se puede completar la replicación inicial en hello especificado tiempo. valor predeterminado de Hello es 72 horas. |
| -User | (Opcional) Hola usuario nombre toouse tooconnect toohello vCenter/servidor de vSphere. Hola se denomina toofetch usado hello más reciente información de configuración de hello las máquinas virtuales, como número de Hola de discos, número de núcleos y número de NIC, toouse en informe de Hola. Si no se proporcionó el nombre de hello, se utiliza la información de configuración de hello recopilada en principio Hola de hello puesta en marcha de generación de perfiles. |
| -Password | Hola (opcional) contraseña toouse tooconnect toohello vCenter server/vSphere host ESXi. Si no se especifica como un parámetro de contraseña de hello, se le pedirá que más adelante cuando se ejecuta el comando Hola. |
| -DesiredRPO | Objetivo de punto de recuperación deseado hello (opcional), en minutos. valor predeterminado de Hello es 15 minutos.|
| -Bandwidth | Ancho de banda en Mbps. toouse toocalculate Hola RPO que se pueden conseguir para Hola de Hello parámetro especifica el ancho de banda. |
| -StartDate | Fecha y hora de inicio hello (opcional) en MM-DD-YYYY:HH:MM (formato de 24 horas). *StartDate* se debe especificar junto con *EndDate*. Cuando se especifica StartDate, informe de Hola se genera para los datos de hello perfiles que se recopilan entre StartDate y EndDate. |
| -EndDate | Fecha de finalización de hello (opcional) y la hora en MM-DD-YYYY:HH:MM (formato de 24 horas). *EndDate* se debe especificar junto con *StartDate*. Cuando se especifica EndDate, se generan informes de Hola para datos de hello perfilada que se recopilan entre StartDate y EndDate. |
| -GrowthFactor | Factor de crecimiento de hello (opcional), expresada como un porcentaje. valor predeterminado de Hello es 30 por ciento. |
| -UseManagedDisks | (Opcional) UseManagedDisks - Yes/No. El valor predeterminado es Yes. número de Hola de máquinas virtuales que puede colocarse en una única cuenta de almacenamiento se calcula teniendo en cuenta que si se realiza la conmutación por error y conmutación por error de máquinas virtuales en un disco administrado en lugar de disk no administrado. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Ejemplo 1: Generar un informe con los valores predeterminados si Hola perfilada datos están almacenados en la unidad local Hola
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Ejemplo 2: Generar un informe una vez datos Hola generar perfiles en un servidor remoto
Debe tener acceso de lectura/escritura en el directorio remoto Hola.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Ejemplo 3: Generar un informe con un toocomplete específico de ancho de banda y objetivo IR dentro de tiempo especificado
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Ejemplo 4: Generar un informe con un factor de crecimiento de un 5 por ciento en lugar de hello predeterminado 30 por ciento
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Ejemplo 5: Generación de un informes con un subconjunto de datos de la generación de perfiles
Por ejemplo, dispone de 30 días de datos del perfil y desea toogenerate un informe de solo 20 días.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Ejemplo 6: Generación de un informes para un RPO de 5 minutos
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Valor del percentil utilizado para el cálculo de Hola
**¿Qué valor de percentil predeterminado Hola de métricas de rendimiento recopilados durante la generación de perfiles hace uso de herramienta de hello cuando genera un informe?**

Hola herramienta toohello 95 percentil valores predeterminados de lectura/escritura de e/s por segundo, escribir IOPS y la renovación de datos que se recopilan durante la generación de perfiles de todas las máquinas virtuales de Hola. Esta métrica asegura de que pico de percentil 100 de hello las máquinas virtuales pueden aparecer debido a eventos temporales es toodetermine no se utiliza en los requisitos de cuenta de almacenamiento y ancho de banda de origen de destino. Por ejemplo, un evento temporal podría ser un trabajo de copia de seguridad que se ejecuta una vez al día, una actividad periódica de indexación de base de datos o de generación de informes de análisis, u otros eventos similares de corta duración que se producen en un momento dado.

Con valores de percentil 95 Hola proporciona que una visión verdadera de características de la carga de trabajo real y le ofrece un rendimiento óptimo cuando se ejecutan cargas de trabajo de hello en Azure. No se prevé que necesitaría toochange este número. Si cambia el valor de hello (de toohello percentil 90, por ejemplo), puede actualizar el archivo de configuración de hello *ASRDeploymentPlanner.exe.config* en Hola carpeta predeterminada y guardarlo toogenerate un nuevo informe de hello existente a perfilar datos.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Consideraciones acerca del factor de crecimiento
**¿Por qué hay que tener en cuenta el factor de crecimiento al planear implementaciones?**

Es tooaccount crítico para el crecimiento de las características de carga de trabajo, suponiendo que un posible aumento de uso con el tiempo. Después de protección en su lugar, si cambian las características de carga de trabajo, no se puede cambiar tooa cuenta de almacenamiento diferente para la protección sin deshabilitar y volver a habilitar la protección de Hola.

Por ejemplo, supongamos que en la actualidad la máquina virtual se ajusta a una cuenta de replicación de almacenamiento estándar. Sobre Hola tres próximos meses, varios cambios son toooccur probable:

* Hola número de usuarios de aplicación Hola que se ejecuta en hello VM aumentará.
* renovación de aumento resultante de Hello en hello VM requerirá toogo toopremium almacenamiento de hello VM para que la replicación de Site Recovery puede mantener el ritmo.
* Por lo tanto, tendrá toodisable y volver a habilitar la cuenta de almacenamiento premium de protección tooa.

Se recomienda encarecidamente que tiene previsto para el crecimiento durante la planificación de la implementación y mientras el valor predeterminado de hello es 30 por ciento. Son Hola experto en sus proyecciones patrón y el crecimiento del uso de aplicación, y puede cambiar este número en consecuencia al generar un informe. Además, puede generar varios informes con varios factores de crecimiento con hello mismo generar perfiles de datos y determinar qué recomendaciones de ancho de banda de origen y de almacenamiento de destino funcionan mejor para usted.

Hola genera informes de Microsoft Excel contiene Hola siguiente información:

* [Entrada](site-recovery-deployment-planner.md#input)
* [Recomendaciones](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Recomendaciones: entrada de ancho de banda](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM&lt;-&gt;Selección de ubicación de almacenamiento](site-recovery-deployment-planner.md#vm-storage-placement)
* [VM compatibles](site-recovery-deployment-planner.md#compatible-vms)
* [VM incompatibles](site-recovery-deployment-planner.md#incompatible-vms)

![Deployment Planner](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>Obtención de rendimiento

rendimiento de Hola de tooestimate Site Recovery puede lograr de tooAzure local durante la replicación, ejecute la herramienta de hello en modo de GetThroughput. herramienta de Hello calcula el rendimiento de Hola desde el servidor de Hola que Hola herramienta se ejecuta en. Idealmente, este servidor se basa en Guía de tamaño del servidor de configuración de Hola. Si ya ha implementado Site Recovery infraestructura componentes locales, ejecute la herramienta de hello en el servidor de configuración de Hola.

Abra una consola de línea de comandos y vaya toohello carpeta de la herramienta de planeación de la implementación en la recuperación del sitio. Ejecute ASRDeploymentPlanner.exe con los siguientes parámetros.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Nombre de parámetro | Descripción |
|-|-|
| -Operation | GetThroughput |
| -Directory | (Opcional) Hola UNC o ruta de acceso del directorio local donde hello Perfilar datos (archivos generados durante la generación de perfiles) se almacena. Estos datos son necesarios para generar informes de Hola. Si no se especifica un nombre de directorio, se utiliza el directorio 'ProfiledData'. |
| -StorageAccountName | nombre de cuenta de almacenamiento de Hola que ha utilizado el ancho de banda toofind Hola consumido para la replicación de datos de tooAzure local. Hola herramienta cargas prueba datos toothis almacenamiento cuenta toofind Hola ancho de banda consumido. |
| -StorageAccountKey | clave de cuenta de almacenamiento de Hola que ha utilizado la cuenta de almacenamiento de tooaccess Hola. Vaya toohello portal de Azure > cuentas de almacenamiento ><*nombre de la cuenta de almacenamiento*>> Configuración > claves de acceso > Key1 (o una clave de acceso principal para una cuenta de almacenamiento clásico). |
| -VMListFile | archivo de Hola que contiene la lista de Hola de toobe de máquinas virtuales de generar un perfil para calcular ancho de banda de hello consumido. ruta de acceso de archivo Hello puede ser absoluta o relativa. archivo Hello debe contener una máquina virtual nombre o dirección IP por línea. nombres de las VM Hola especificados en el archivo hello debe ser Hola igual que los nombres de las VM hello en el host de hello vCenter server/vSphere ESXi.<br>Por ejemplo, el archivo hello VMList.txt contiene Hola después de las máquinas virtuales:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (Opcional) Se trata del entorno de la cuenta de Azure Storage de destino. Puede ser uno de estos tres valores: AzureCloud, AzureUSGovernment y AzureChinaCloud. El valor predeterminado es AzureCloud. Use el parámetro de hello cuando la región de Azure de destino es nubes Azure gobierno de Estados Unidos o en Azure China. |

herramienta de Hello crea varios 64 MB asrvhdfile <> # .vhd archivos (donde "#" es el número de Hola de archivos) en el directorio especificado Hola. herramienta de Hello carga Hola archivos toohello almacenamiento cuenta toofind Hola el rendimiento. Después de que se mide el rendimiento de hello, herramienta de hello elimina todos los archivos de Hola de cuenta de almacenamiento de Hola y de servidor local de Hola. Si por algún motivo finaliza herramienta Hola mientras está calculando el rendimiento, no elimina archivos de Hola de almacenamiento de Hola o de servidor local de Hola. Tendrá toodelete ellos manualmente.

Hello el rendimiento se mide en un punto determinado en el tiempo y es el rendimiento máximo Hola que puede lograr la recuperación del sitio durante la replicación, siempre que todos los demás factores son iguales Hola. Por ejemplo, si cualquier aplicación comienza a consumir más ancho de banda en hello varía en la misma red, el rendimiento real de Hola durante la replicación. Si está ejecutando hello GetThroughput comando desde un servidor de configuración, la herramienta de hello es consciente de las máquinas virtuales protegidas y la replicación en curso. Hello resultados de rendimiento medido hello es distinto si hello GetThroughput la operación se ejecutará cuando Hola proteger las máquinas virtuales tiene datos de alta renovación. Se recomienda ejecutar herramienta hello en varios puntos en el tiempo durante la generación de perfiles toounderstand qué rendimiento se pueden alcanzar niveles en momentos diferentes. En el informe de hello, herramienta de hello muestra rendimiento medido último de Hola.

### <a name="example"></a>Ejemplo
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Ejecutar la herramienta de hello en un servidor que tenga Hola mismo almacenamiento y las características de la CPU como servidor de configuración de Hola.
>
> En la replicación, conjunto Hola recomienda Hola de ancho de banda toomeet RPO 100% del tiempo de Hola. Después de establecer el ancho de banda de derecho hello, si no ve aumentar el rendimiento de hello logra notificado por herramienta Hola de, Hola siguientes:
>
>  1. Compruebe toodetermine si no hay ninguna red de calidad de servicio (QoS) que se está limitando el rendimiento de recuperación del sitio.
>
>  2. Compruebe toodetermine si se encuentra el almacén de Site Recovery en hello más cercano de latencia de red de toominimize de región de Microsoft Azure físicamente admitida.
>
>  3. Compruebe su toodetermine de las características de almacenamiento local si se puede mejorar el hardware de hello (por ejemplo, unidad de disco duro tooSSD).
>
>  4. Cambiar la configuración de Site Recovery de hello en el servidor de procesos de hello demasiado[aumentar la cantidad de Hola de ancho de banda de red utilizado para la replicación](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Recomendaciones con el RPO deseado como entrada

### <a name="profiled-data"></a>Datos de generación de perfiles

![vista de datos de perfiles de Hello en planes de implementación de Hola](./media/site-recovery-deployment-planner/profiled-data-period.png)

**Período de datos del perfil**: período de Hola durante qué Hola se ejecutó la generación de perfiles. De forma predeterminada, herramienta de hello incluye todos los datos del perfil en el cálculo de hello, a menos que genera informes de Hola durante un período específico mediante opciones StartDate y EndDate durante la generación de informes.

**Nombre del servidor**: nombre de Hola o dirección IP de hello VMware vCenter o host ESXi se genera el informe cuyo máquinas virtuales.

**Deseado RPO**: objetivo de punto de recuperación de hello para la implementación. De forma predeterminada, Hola requiere ancho de banda de red se calcula para los valores RPO de 15, 30 y 60 minutos. En función de selección de hello, valores de hello afectado se actualizan en la hoja de Hola. Si ha usado hello *DesiredRPOinMin* parámetro durante la generación de informes de hello, que se muestra el valor de resultado deseado RPO de Hola.

### <a name="profiling-overview"></a>Información general sobre la generación de perfiles

![Resultados de la generación de perfiles en planes de implementación de Hola](./media/site-recovery-deployment-planner/profiling-overview.png)

**Total de máquinas virtuales de perfiles**: Hola número total de máquinas virtuales cuyos datos del perfil están disponibles. Si hello VMListFile tiene los nombres de todas las máquinas virtuales que no se han perfilar, esas máquinas virtuales no se consideran en la generación de informes de Hola y se excluyen de recuento de hello total para las máquinas virtuales.

**Máquinas virtuales compatibles**: Hola número de máquinas virtuales que pueden ser tooAzure protegido mediante el uso de Site Recovery. Es Hola número total de máquinas virtuales compatibles para qué Hola se calculan el ancho de banda de red requeridos, número de cuentas de almacenamiento, número de núcleos de Azure y número de servidores de configuración y los servidores de procesos adicionales. Hola detalles de cada máquina virtual compatible están disponibles en la sección "Máquinas virtuales compatibles" Hola.

**Máquinas virtuales incompatible**: Hola número de máquinas virtuales para que no son compatibles con la protección con recuperación de sitio. motivos de Hola para incompatibilidad que se indican en la sección "Máquinas virtuales Incompatible" Hola. Si hello VMListFile tiene nombres de todas las máquinas virtuales no se generan perfiles, esas máquinas virtuales se excluyen de recuento de máquinas virtuales de hello incompatible. Estas máquinas virtuales se muestran como "Datos no encontraron" al final de Hola de sección Hola "VMs Incompatible".

**RPO deseado**: el objetivo del punto de recuperación deseado, en minutos. informe de Hola se genera para los tres valores RPO: 15 (valor predeterminado), 30 y 60 minutos. recomendación de ancho de banda de Hello en el informe de Hola se cambia en función de su selección en la lista Hola desplegable RPO deseado en hello parte superior derecha de la hoja de Hola. Si ha generado el informe de hello mediante el uso de hello *DesiredRPO -* parámetro con un valor personalizado, este valor personalizado se mostrará como valor predeterminado de hello en lista de hello deseado RPO de lista desplegable.

### <a name="required-network-bandwidth-mbps"></a>Ancho de banda de red requerido (Mbps)

![Ancho de banda de red necesario en planes de implementación de Hola](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100% del tiempo de hello:** Hola recomienda ancho de banda en Mbps toobe asignada toomeet el RPO deseado 100% del tiempo de Hola. Esta cantidad de ancho de banda debe ser dedicado para la replicación de datos de estado estable de todos los tooavoid máquinas virtuales compatible las infracciones de RPO.

**toomeet RPO 90 por ciento de tiempo de Hola**: debido a precios de banda ancha o por cualquier otra razón, si no se establece toomeet de ancho de banda necesario Hola el RPO deseado 100% del tiempo de hello, puede elegir toogo con un ancho de banda inferior configuración pueda cumplir su RPO deseado 90 por ciento del tiempo de presentación. implicaciones de hello toounderstand de establecer este ancho de banda inferior, informe de hello proporciona un análisis de escenarios condicionales en número de Hola y la duración de RPO infracciones tooexpect.

**El rendimiento obtenido:** rendimiento de Hola desde el servidor de hello en el que ha ejecutado región hello GetThroughput comando toohello Microsoft Azure donde se encuentra la cuenta de almacenamiento de Hola. Este número de rendimiento indica el nivel de hello estimado que se puede lograr si se protege Hola Hola compatible con máquinas virtuales mediante el uso de recuperación del sitio, siempre que el servidor de configuración o características de almacenamiento y de red del servidor de proceso permanecen igual que servidor de Hola desde el que se ha ejecutado la herramienta de Hola.

En la replicación, debe establecer hello toomeet Hola recomendada de ancho de banda RPO 100% del tiempo de Hola. Después de establecer el ancho de banda de hello, si no ve algún aumento en el rendimiento de hello logra, devuelto por la herramienta de hello, realice Hola siguientes:

1. Compruebe toosee si no hay ninguna red de calidad de servicio (QoS) que se está limitando el rendimiento de recuperación del sitio.

2. Compruebe toosee si se encuentra el almacén de Site Recovery en hello más cercano de latencia de red de toominimize de región de Microsoft Azure físicamente admitida.

3. Compruebe su toodetermine de las características de almacenamiento local si se puede mejorar el hardware de hello (por ejemplo, unidad de disco duro tooSSD).

4. Cambiar la configuración de Site Recovery de hello en el servidor de procesos de hello demasiado[aumentar usada para la replicación el ancho de banda de red a cantidad de hello](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Si está ejecutando la herramienta de hello en un servidor de configuración o proceso que ya ha protegido las máquinas virtuales, ejecute herramienta Hola varias veces. Hola conseguido rendimiento número cambia según la cantidad de Hola de renovación está procesando en ese momento en el tiempo de.

Para todas las implementaciones de Site Recovery que se realicen en la empresa, se recomienda usar [ExpressRoute](https://aka.ms/expressroute).

### <a name="required-storage-accounts"></a>Cuentas de almacenamiento requeridas
Hola siguiente gráfico se muestra las cuentas de número total de Hola de almacenamiento (standard y premium) que son necesario tooprotect todos los Hola máquinas virtuales compatibles. toolearn qué almacenamiento cuenta toouse para cada máquina virtual, vea la sección de "selección de ubicación de almacenamiento de máquina virtual" de Hola.

![Cuentas de almacenamiento necesaria en planes de implementación de Hola](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Número de núcleos de Azure requeridos
Este resultado es número total de Hola de toobe núcleos configurar antes de Hola de conmutación por error de conmutación por error o prueba de todas las máquinas virtuales compatibles. Si muy pocos núcleos disponibles en la suscripción de hello, Site Recovery se produce un error toocreate las máquinas virtuales en tiempo de Hola de conmutación por error o conmutación por error de prueba.

![Número necesario de Azure núcleos en planes de implementación de Hola](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Infraestructura local requerida
Esta ilustración es el número total de Hola de servidores de configuración y toobe de servidores de proceso adicionales configurados que sería suficiente tooprotect todos Hola máquinas virtuales compatibles. Función hello admitida [cambiar el tamaño de las recomendaciones para el servidor de configuración de Hola](https://aka.ms/asr-v2a-on-prem-components), herramienta de hello podría recomendar servidores adicionales. Hola recomendación se basa en hello mayor de renovación al día de Hola o número máximo de Hola de máquinas virtuales protegidas (suponiendo un promedio de tres discos por máquina virtual), lo que se alcance primero en el servidor de configuración de Hola o servidor de proceso adicional de Hola. Encontrará detalles de Hola de renovación total por día y el número total de discos protegidos en la sección "Entrada" Hola.

![Infraestructura local necesaria en planes de implementación de Hola](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Análisis de hipótesis
Este análisis describen podrían producir infracciones de cuántos durante Hola al establecer el período de generación de perfiles que un bajo ancho de banda para hello deseado RPO toobe cumple sólo el 90 por ciento del tiempo de presentación. Pueden producirse una o varias infracciones de RPO en cualquier día determinado. gráfico de Hello muestra pico Hola RPO del día de Hola.
En función de este análisis, puede decidir si el número de Hola de infracciones de RPO entre todos los días y una memoria máxima RPO visitas al día es aceptable con hello especificado bajo ancho de banda. Si es aceptable, puede asignar ancho de banda inferior hello para la replicación, else asignar Hola mayor ancho de banda toomeet sugerido Hola había deseado RPO 100% del tiempo de Hola.

![Análisis de escenarios condicionales en planes de implementación de Hola](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>Tamaño de lote de máquinas virtuales recomendado para la replicación inicial
En esta sección, se recomienda número Hola de máquinas virtuales que se pueden proteger en la replicación inicial de hello toocomplete paralelas dentro de 72 horas con hello sugiere toomeet de ancho de banda deseado RPO 100% del tiempo de Hola que se va a establecer. Este valor se puede configurar. toochange en tiempo de generación de informes, use hello *GoalToCompleteIR* parámetro.

gráfico aquí Hello muestra un intervalo de valores de ancho de banda y una calculada VM lote tamaño recuento toocomplete la replicación inicial en 72 horas, según promedio de hello detecta VM Hola de tamaño en todas las máquinas virtuales compatibles.

En la versión preliminar pública de hello, informe de hello no especifica qué máquinas virtuales deben incluirse en un lote. Puede usar el tamaño del disco Hola que se muestra de Hola "compatible con máquinas virtuales" sección toofind tamaño de cada VM y seleccionarlos para un lote, o puede seleccionar máquinas virtuales de hello basadas en las características de carga de trabajo conocidos. hora de finalización de Hola de cambios de la replicación inicial de hello proporcionalmente, según el tamaño de disco de máquina virtual real de hello, utiliza espacio en disco y el rendimiento de red disponible.

![Tamaño de lote de máquinas virtuales recomendado](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Factor de crecimiento y valores de percentil utilizados
En esta sección final Hola de hello hoja se utiliza para todos los contadores de rendimiento de Hola de máquinas virtuales de hello Perfilar (el valor predeterminado es el percentil 95) de valor del percentil de muestra Hola y Hola factor de crecimiento (el valor predeterminado es 30 por ciento) que se utiliza en todos los cálculos de Hola.

![Factor de crecimiento y valores de percentil utilizados](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Recomendaciones relacionadas con el ancho de banda disponible como entrada

![Recomendaciones relacionadas con el ancho de banda disponible como entrada](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Puede darse el caso de que sepa que no puede establecer un ancho de banda de más de x Mbps para la replicación de Site Recovery. herramienta de Hello permite tooinput ancho de banda disponible (usando Hola - parámetro de ancho de banda durante la generación de informes) y get Hola factible RPO en minutos. Con este valor RPO factible, puede decidir si necesita tooset el ancho de banda adicional o están bien con tener una solución de recuperación ante desastres con este RPO.

![RPO factible para un ancho de banda de 500 Mbps](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Entrada
hoja de cálculo de entrada de Hello proporciona que una visión general de hello Perfilar entorno de VMware.

![Información general de hello Perfilar entorno de VMware](./media/site-recovery-deployment-planner/Input.png)

**Fecha de inicio** y **fecha de finalización**: Hola fechas de inicio y finalización del programa Hola tienen en cuenta para la generación de informes de datos de generación de perfiles. De forma predeterminada, fecha de inicio de hello es la fecha de hello cuando de generación de perfiles se inicia, y fecha de finalización de hello es fecha hello cuando se detiene la generación de perfiles. Esto puede ser hello 'StartDate' y 'EndDate' valores si se genera el informe de hello con estos parámetros.

**Número total de días de generación de perfiles**: número total de Hola de días de generación de perfiles entre Hola fechas inicial y final para qué Hola se genera el informe.

**Número de máquinas virtuales compatibles**: número total de Hola de máquinas virtuales compatibles para qué ancho de banda de red de hello necesario, el número necesario de almacenamiento cuentas, núcleos de Microsoft Azure, servidores de configuración y son servidores de procesos adicionales calcula.

**Número total de discos a través de todas las máquinas virtuales compatibles**: número de Hola que se usa como uno de hello entradas número de hello toodecide de servidores de configuración y toobe de servidores de proceso adicionales utilizados en la implementación de Hola.

**Promedio de discos por máquina virtual compatibles**: promedio de Hola de discos se calcula en todas las máquinas virtuales compatibles.

**Promedio de tamaño de disco (GB)**: calcular el tamaño de disco promedio de hello en todas las máquinas virtuales compatibles.

**Deseado RPO (minutos)**: cualquier Hola recuperación punto objetivo o hello pasa valor predeterminado para el parámetro de 'DesiredRPO' hello en tiempo de Hola de tooestimate de generación de informes requerido ancho de banda.

**Deseado de ancho de banda (Mbps)**: Hola valor que ha pasado para el parámetro de 'Ancho de banda' hello en tiempo de Hola de tooestimate de generación de informes RPO factible.

**Renovación de datos típico observado por día (GB)**: Hola renovación de datos medio se observa en todos los perfiles de días. Este número se utiliza como uno de hello entradas toodecide Hola serie de servidores de configuración y toobe de servidores de proceso adicionales utilizados en la implementación de Hola.


## <a name="vm-storage-placement"></a>Selección de ubicación de almacenamiento de máquina virtual

![Selección de ubicación de almacenamiento de máquina virtual](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Tipo de almacenamiento en disco**: una cuenta de almacenamiento standard o premium, que es usado tooreplicate todos Hola correspondientes máquinas virtuales que se mencionó en hello **tooPlace de máquinas virtuales** columna.

**Sugiere prefijo**: sugerido prefijo de tres caracteres de Hola que puede usarse para asignar nombres de cuenta de almacenamiento de Hola. Puede usar su propio prefijo, pero las sugerencias de la herramienta de hello sigue hello [convención de nomenclatura para las cuentas de almacenamiento de partición](https://aka.ms/storage-performance-checklist).

**Sugiere el nombre de la cuenta**: nombre de la cuenta de almacenamiento de hello después de incluir el prefijo sugerido Hola. Reemplace el nombre de hello dentro de corchetes angulares de hello (< y >) con la entrada personalizada.

**Cuenta de almacenamiento de registro**: todos los registros de replicación de Hola se almacenan en una cuenta de almacenamiento estándar. Para las máquinas virtuales que se replican tooa cuenta de almacenamiento premium, configure una cuenta de almacenamiento estándar adicional para el almacenamiento de registro. Varias cuentas de almacenamiento de replicación Premium puede usar una única cuenta de almacenamiento de registros Estándar. Las máquinas virtuales que son usan cuentas de almacenamiento de toostandard replicada Hola misma cuenta de almacenamiento para los registros.

**Sugiere el nombre de la cuenta de registro**: el nombre de cuenta de registro de almacenamiento después de incluir el prefijo sugerido Hola. Reemplace el nombre de hello dentro de corchetes angulares de hello (< y >) con la entrada personalizada.

**Resumen de la selección de ubicación**: un resumen de hello total de carga de máquinas virtuales en la cuenta de almacenamiento de hello en tiempo de presentación de la replicación y probar la conmutación por error o conmutación por error. Incluye el número total de Hola de las máquinas virtuales asignadas toohello cuenta de almacenamiento total de lectura/escritura (replicación) IOPS, tamaño total del programa de instalación en todos los discos y el número total de discos de escritura de e/s por segundo en todas las máquinas virtuales que se colocan en esta cuenta de almacenamiento total.

**Máquinas virtuales tooPlace**: Hola a una lista de todas las máquinas virtuales que se deben colocar en hello dado cuenta de almacenamiento para un rendimiento óptimo y uso.

## <a name="compatible-vms"></a>Máquinas virtuales compatibles
![Hoja de cálculo de Excel de las máquinas virtuales compatibles](./media/site-recovery-deployment-planner/compatible-vms.png)

**Nombre de máquina virtual**: Hola nombre de máquina virtual o la dirección IP que se utiliza en hello VMListFile cuando se genera un informe. Esta columna también muestra los discos de hello (VMDK) que están conectados toohello las máquinas virtuales. toodistinguish vCenter máquinas virtuales con nombres duplicados o las direcciones IP, nombres de hello incluir nombre de host ESXi Hola. Hello enumerado host ESXi es hello uno donde hello VM se colocó al herramienta Hola detectados durante el período de generación de perfiles de Hola.

**Compatibilidad de máquina virtual**: los valores son **Sí** y **Sí**\*. **Sí** \* es para instancias de en qué Hola VM es una opción para [almacenamiento de Azure Premium](https://aka.ms/premium-storage-workload). En este caso, Hola Perfilar alta renovación o disco IOPS se ajusta a Hola P20 o categoría de P30, pero tamaño Hola del disco de hello hace que toobe asignado hacia abajo tooa P10 o P20. cuenta de almacenamiento de Hello decide qué disco de almacenamiento premium escriba toomap un disco, en función de su tamaño. Por ejemplo:
* Menos de 128 GB es P10.
* 128 GB too512 GB es un P20.
* 512 GB too1024 GB es un P30.
* 1025 GB too2048 GB es un P40.
* GB too4095 GB es un P50 2049.

Si las características de la carga de trabajo de Hola de un disco colocan en Hola P20 o P30 categoría, pero tamaño Hola lo asigna hacia abajo el tipo de disco de almacenamiento de inferior premium de tooa, herramienta de hello marca esa máquina virtual como **Sí**\*. herramienta de Hello también se recomienda cambiar toofit de tamaño de disco de origen de hello en hello recomendada el tipo de disco de almacenamiento premium o cambiar Hola destino disco tipo post-conmutación por error.

**Tipo de almacenamiento**: Estándar o Premium.

**Sugiere prefijo**: prefijo de la cuenta de almacenamiento de tres caracteres de Hola.

**Cuenta de almacenamiento**: nombre de Hola que utiliza el prefijo de hello sugerido de cuenta de almacenamiento.

**IOPS de lectura/escritura (con el Factor de crecimiento)**: Hola de máxima carga de trabajo lectura/escritura e/s por segundo en el disco de hello (el valor predeterminado es percentil 95), incluidos el factor de crecimiento futuro de hello (el valor predeterminado es 30 por ciento). Tenga en cuenta que Hola total lectura/escritura de e/s por segundo de una máquina virtual no es siempre suma de Hola de IOPS de lectura/escritura de discos individuales de la máquina virtual de hello, porque Hola pico lectura/escritura IOPS de hello VM es pico de Hola de suma de Hola de sus discos individuales lectura/escritura IOPS durante cada minuto de hello período de generación de perfiles.

**Renovación de datos en Mbps (con el Factor de crecimiento)**: tasa de renovación de pico de hello en el disco de hello (el valor predeterminado es percentil 95), incluidos el factor de crecimiento futuro de hello (el valor predeterminado es 30 por ciento). Tenga en cuenta que Hola renovación total de los datos del programa Hola a máquina virtual no es siempre suma Hola de renovación de datos de discos individuales de la máquina virtual de hello porque renovación de datos máxima de Hola de hello VM es pico de Hola de suma de Hola de renovación de sus discos individuales durante cada minuto de hello período de generación de perfiles.

**Tamaño de la máquina virtual de Azure**: Hola ideal asignado tamaño de máquina virtual de servicios en la nube para este servidor local de máquina virtual. asignación de Hola basada en la memoria de la VM de hello en local, número de núcleos de discos/NIC y lectura/escritura de e/s por segundo. recomendación de Hello es siempre menor tamaño de máquina virtual de Azure de Hola que se ajusta a todas las características de máquina virtual de hello local.

**Número de discos**: Hola número total de discos de máquina virtual (VMDK) en hello máquina virtual.

**Tamaño (GB) de disco**: Hola tamaño total del programa de instalación de todos los discos del programa Hola a máquina virtual. herramienta Hello también muestra el tamaño del disco Hola de discos individuales de Hola de hello VM.

**Núcleos**: número de Hola de CPU de núcleos en hello VM.

**Memoria (MB)**: Hola RAM en hello máquina virtual.

**NIC**: Hola número de tarjetas NIC en hello máquina virtual.

**Tipo de arranque**: es de tipo de inicio del programa Hola a máquina virtual. Puede ser BIOS o EFI. Actualmente, Azure Site Recovery admite solo el tipo de arranque BIOS. Todas las máquinas virtuales de Hola de tipo de arranque EFI se muestran en la hoja de cálculo de máquinas virtuales Incompatible.

**Tipo de sistema operativo**: hello es el tipo de sistema operativo de hello máquina virtual. Puede ser Windows, Linux u otro.

## <a name="incompatible-vms"></a>Máquinas virtuales no compatibles

![Hoja de cálculo de Excel de máquinas virtuales no compatibles](./media/site-recovery-deployment-planner/incompatible-vms.png)

**Nombre de máquina virtual**: Hola nombre de máquina virtual o la dirección IP que se utiliza en hello VMListFile cuando se genera un informe. Esta columna también muestra los archivos VMDK Hola que están conectados toohello las máquinas virtuales. toodistinguish vCenter máquinas virtuales con nombres duplicados o las direcciones IP, nombres de hello incluir nombre de host ESXi Hola. Hello enumerado host ESXi es hello uno donde hello VM se colocó al herramienta Hola detectados durante el período de generación de perfiles de Hola.

**Compatibilidad de la máquina virtual**: indica por qué Hola dada la máquina virtual no es compatible para su uso con Site Recovery. Hello motivos se describen para cada disco incompatible de hello VM y, según se publican en [límites de almacenamiento](https://aka.ms/azure-storage-scalbility-performance), puede ser cualquiera de los siguientes hello:

* El tamaño del disco es superior a 4095 GB. Azure Storage no admite actualmente discos de datos cuyo tamaño supere 4095 GB.
* El tamaño del disco de sistema operativo es superior a 2048 GB. Azure Storage no admite actualmente discos de sistema operativo cuyo tamaño supere 2048 GB.
* El tipo de arranque es EFI. Azure Site Recovery actualmente solo admite máquinas virtuales con tipo de arranque BIOS.

* Tamaño total de VM (replicación + TFO) supera el límite de tamaño de cuenta de almacenamiento de hello admitida (35 TB). Esta incompatibilidad se produce normalmente cuando un solo disco Hola VM tiene una característica de rendimiento que supera hello Azure o recuperación del sitio de los límites máximos admitidos para el almacenamiento estándar. Una instancia de este tipo inserta Hola VM en la zona de almacenamiento premium de Hola. Sin embargo, no se puede proteger Hola máximo tamaño admitido de una cuenta de almacenamiento premium es 35 TB y protegidos de una sola máquina virtual a través de varias cuentas de almacenamiento. Tenga en cuenta también que cuando una conmutación por error de prueba se ejecuta en una máquina virtual protegida, se ejecuta en Hola donde está progresando replicación misma cuenta de almacenamiento. En este caso, configure 2 x tamaño Hola del disco de Hola para replicación tooprogress y probar la conmutación por error toosucceed en paralelo.
* El valor de IOPS de origen supera el límite que admite el almacenamiento, 5000 por disco.
* El valor de IOPS de origen supera el límite que admite el almacenamiento, 80 000 por máquina virtual.
* Renovación de datos medio supera el límite admitido de renovación de datos de Site Recovery de 10 MBps para el tamaño promedio de E/S de disco de Hola.
* Renovación de datos total en todos los discos en hello VM supera el límite de renovación de datos de Site Recovery de hello máximo compatible de 54 MBps por máquina virtual.
* IOPS de escritura efectivo medio supera el límite de IOPS de recuperación de sitio de hello compatible de 840 para el disco.
* Almacenamiento de instantáneas calculado supera el límite de almacenamiento de instantáneas de hello compatible de 10 TB.

**IOPS de lectura/escritura (con el Factor de crecimiento)**: Hola cargas máximas de trabajo e/s por segundo en el disco de hello (el valor predeterminado es percentil 95), incluidos el factor de crecimiento futuro de hello (el valor predeterminado es 30 por ciento). Tenga en cuenta que Hola total lectura/escritura de e/s por segundo de hello VM no es siempre suma de Hola de IOPS de lectura/escritura de discos individuales de la máquina virtual de hello, porque Hola pico lectura/escritura IOPS de hello VM es pico de Hola de suma de Hola de sus discos individuales lectura/escritura IOPS durante cada minuto de hello período de generación de perfiles.

**Renovación de datos en Mbps (con el Factor de crecimiento)**: tasa de renovación de pico de hello en el disco de hello (percentil 95 predeterminada) incluyendo el factor de crecimiento futuro de hello (valor predeterminado 30 por ciento). Tenga en cuenta que Hola renovación total de los datos del programa Hola a máquina virtual no es siempre suma Hola de renovación de datos de discos individuales de la máquina virtual de hello porque renovación de datos máxima de Hola de hello VM es pico de Hola de suma de Hola de renovación de sus discos individuales durante cada minuto de hello período de generación de perfiles.

**Número de discos**: Hola número total de archivos VMDK en hello máquina virtual.

**Tamaño (GB) de disco**: Hola tamaño total del programa de instalación de todos los discos del programa Hola a máquina virtual. herramienta Hello también muestra el tamaño del disco Hola de discos individuales de Hola de hello VM.

**Núcleos**: número de Hola de CPU de núcleos en hello VM.

**Memoria (MB)**: cantidad Hola de memoria RAM Hola máquina virtual.

**NIC**: Hola número de tarjetas NIC en hello máquina virtual.

**Tipo de arranque**: es de tipo de inicio del programa Hola a máquina virtual. Puede ser BIOS o EFI. Actualmente, Azure Site Recovery admite solo el tipo de arranque BIOS. Todas las máquinas virtuales de Hola de tipo de arranque EFI se muestran en la hoja de cálculo de máquinas virtuales Incompatible.

**Tipo de sistema operativo**: hello es el tipo de sistema operativo de hello máquina virtual. Puede ser Windows, Linux u otro.


## <a name="site-recovery-limits"></a>Límites de Site Recovery

**Destino de almacenamiento de la replicación** | **Tamaño medio de E/S de disco de origen** |**Actividad de datos media de disco de origen** | **Actividad de datos de disco de origen total por día**
---|---|---|---
Standard storage | 8 KB | 2 MBps | 168 GB por disco
Disco P10 Premium | 8 KB | 2 MBps | 168 GB por disco
Disco P10 Premium | 16 KB | 4 MBps | 336 GB por disco
Disco P10 Premium | 32 KB, o más | 8 MBps | 672 GB por disco
Disco Premium P20 o P30 | 8 KB  | 5 MBps | 421 GB por disco
Disco Premium P20 o P30 | 16 KB, o más |10 MBps | 842 GB por disco

Estos son los números promedio si la superposición de E/S es del 30 %. Site Recovery es capaz de controlar un mayor rendimiento en función de la relación de superposición, tamaños de escritura mayores y el comportamiento real de E/S de la carga de trabajo. Hello números anteriores supone un trabajo pendiente típico de aproximadamente cinco minutos. Es decir, una vez que se cargan los datos, se procesan y se crea un punto de recuperación en menos de cinco minutos.

Estos límites se basan en nuestras pruebas, pero no pueden cubrir todas las combinaciones de E/S posibles de la aplicación. Los resultados reales pueden variar en función de la combinación de E/S de la aplicación. Para obtener mejores resultados, incluso después de la planificación de la implementación, siempre recomendamos que realice una amplia aplicación pruebas mediante una imagen de prueba de conmutación por error tooget Hola rendimiento true.

## <a name="updating-hello-deployment-planner"></a>Planificador de implementación de actualización Hola
planes de implementación de hello tooupdate, Hola siguientes:

1. Descargar Hola la versión más reciente de hello [planificador de implementación de Azure Site Recovery](https://aka.ms/asr-deployment-planner).

2. Copia Hola .zip carpeta tooa el servidor que desea que toorun en.

3. Extraiga la carpeta de .zip Hola.

4. Realice una de las siguientes de hello:
 * Si la versión más reciente de hello no contiene una corrección de generación de perfiles y de generación de perfiles ya está en curso en la versión actual del programador de hello, continuar Hola de generación de perfiles.
 * Si la versión más reciente de hello contienen una corrección de generación de perfiles, se recomienda que detener la generación de perfiles en su versión actual y reinicie Hola de generación de perfiles con la nueva versión de hello.

  >[!NOTE]
  >
  >Al iniciar la generación de perfiles con hello nueva versión, pase Hola que misma ruta de acceso del directorio de salida para que hello herramienta anexa datos de perfil en Hola archivos existentes. Será un conjunto completo de datos del perfil usa informes de hello toogenerate. No se usa si pasa un directorio de salida diferente, se crean nuevos archivos y antiguo perfiles de datos de informe de hello toogenerate.
  >
  >Cada nuevo programador de implementación es una actualización acumulativa del archivo .zip de Hola. No es necesario toocopy hello más reciente archivos toohello carpeta anterior. Se puede crear y usar una carpeta nueva.


## <a name="version-history"></a>Historial de versiones

### <a name="131"></a>1.3.1
Última actualización: 19 de julio de 2017

Se agrega la siguiente característica nueva:

* Se agregó compatibilidad con discos de gran tamaño (> 1TB) en la generación de informes. Ahora puede utilizar la implementación planner tooplan replicación para máquinas virtuales que tengan tamaños de disco superiores a 1 TB (hasta 4095 GB).
Para más información, consulte [Compatibilidad con discos de gran tamaño en Azure Site Recovery](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1.3
Actualización: 9 de mayo de 2017

Se agrega la siguiente característica nueva:

* Se ha agregado la compatibilidad con discos administrados en la generación de informes. Hello número de máquinas virtuales se puede colocar tooa único almacenamiento cuenta es calculada en función de si administra el disco está seleccionada para la conmutación por error y conmutación por error.        


### <a name="12"></a>1.2
Actualización: 7 de abril de 2017

Se han agregado las revisiones siguientes:

* Arranque agregado escriba comprobación (BIOS o EFI) para cada máquina virtual toodetermine si la máquina virtual de hello es compatible o incompatible para la protección de Hola.
* SO agregado escriba información para cada máquina virtual en hello compatibles de las máquinas virtuales y hojas de cálculo de máquinas virtuales Incompatible.
* Hola GetThroughput operación ahora es compatible con las regiones de gobierno de Estados Unidos y en Microsoft Azure de China Hola.
* Se han agregado algunas comprobaciones más de requisitos previos para el servidor vCenter y ESXi.
* Se estén generando informe incorrecto cuando la configuración regional se establece toonon en inglés.


### <a name="11"></a>1.1
Actualización: 9 de marzo de 2017

Hola fijo problemas siguientes:

* herramienta de Hello no puede generar perfiles máquinas virtuales si vCenter hello tiene dos o más máquinas virtuales con Hola el mismo nombre o dirección IP a través de varios hosts de ESXi.
* Copia y la búsqueda está deshabilitada para hojas de cálculo de hello compatibles de las máquinas virtuales y máquinas virtuales Incompatible.

### <a name="10"></a>1.0
Actualización: 23 de febrero de 2017

Azure planificador de implementación de recuperación de sitio public preview de 1.0 tiene siguientes de hello conocidos problemas (toobe tratada en las próximas actualizaciones):

* herramienta de Hello solo funciona para escenarios de VMware en Azure, no para las implementaciones de Hyper-V en Azure. Para escenarios de Hyper-V en Azure, use hello [herramienta de planificación de capacidad de Hyper-V](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Hola GetThroughput operación no se admite en las regiones de gobierno de Estados Unidos y en Microsoft Azure de China Hola.
* herramienta Hello no puede generar perfiles de las máquinas virtuales si el servidor de vCenter hello tiene dos o más máquinas virtuales con Hola el mismo nombre o dirección IP a través de varios hosts de ESXi. En esta versión, herramienta de hello omite la generación de perfiles para los nombres duplicados de VM o direcciones IP en hello VMListFile. solución de Hello es tooprofile Hola máquinas virtuales mediante el uso de un host ESXi en lugar de servidor de vCenter Hola. Debe ejecutar una instancia para cada host de ESXi.
