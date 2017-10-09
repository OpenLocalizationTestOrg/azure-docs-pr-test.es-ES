Máquinas virtuales (VM) Azure podría reiniciarse a veces sin motivo aparente, sin la evidencia de su habiendo iniciado operación de reinicio de Hola. Este artículo enumeran las acciones de Hola y eventos que pueden ocasionar tooreboot de máquinas virtuales y proporciona una visión general de cómo tooavoid inesperado reiniciar problemas o reducir el impacto de Hola de dichos problemas.

## <a name="configure-hello-vms-for-high-availability"></a>Configurar máquinas virtuales de Hola para lograr alta disponibilidad
Hola mejor manera tooprotect una aplicación que se ejecuta en Azure con VM se reinicia y el tiempo de inactividad es tooconfigure hello las máquinas virtuales de alta disponibilidad.

tooprovide este nivel de aplicación de tooyour de redundancia, le recomendamos que agrupe dos o más máquinas virtuales en un conjunto de disponibilidad. Esta configuración garantiza que durante un evento de mantenimiento planeado o no, al menos una máquina virtual esté disponible y cumple Hola 99,95 por ciento [SLA de Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Para obtener más información acerca de los conjuntos de disponibilidad, vea Hola siguientes artículos:

- [Administrar la disponibilidad de Hola de máquinas virtuales](../articles/virtual-machines/windows/manage-availability.md)
- [Configuración de un conjunto de disponibilidad para máquinas virtuales con Windows en el modelo de implementación clásica](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Información acerca de Resource Health 
Mantenimiento de recursos de Azure es un servicio que expone el estado de hello individuales de recursos de Azure y proporciona una guía útil para solucionar problemas. En un entorno de nube donde no es posible toodirectly servidores de acceso o elementos de la infraestructura, objetivo de hello del mantenimiento de recursos es hora de hello tooreduce que tiene que dedicar sobre cómo solucionar problemas. En concreto, objetivo de hello es tiempo de hello tooreduce empleado en la determinación de si raíz Hola de problema de Hola encuentra en la aplicación hello o en un evento dentro de hello plataforma Windows Azure. Para más información, consulte la [introducción al uso de Resource Health](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Las acciones y eventos que pueden causar Hola tooreboot VM

### <a name="planned-maintenance"></a>Mantenimiento planeado
Microsoft Azure realiza periódicamente actualizaciones a través de confiabilidad de Hola mundo tooimprove hello, rendimiento y seguridad de la infraestructura de host de Hola que subyace a las máquinas virtuales. Muchas de esas actualizaciones, entre las que se incluyen las de conservación de memoria, se realizan sin que afecten a las máquinas virtuales ni a los servicios en la nube.

Sin embargo, algunas de ellas requieren un reinicio. En tales casos, el Hola las máquinas virtuales se apagan mientras se patch infraestructura hello y, a continuación, se reinician hello las máquinas virtuales.

toounderstand es el mantenimiento planificado de Azure y cómo puede afectar a la disponibilidad de Hola de las máquinas virtuales de Linux, consulte los artículos de hello enumerados aquí. artículos de Hello proporcionan información general sobre el proceso de mantenimiento planificado de Azure de Hola y cómo tooschedule planeada mantenimiento toofurther reducen el impacto de Hola.

- [Mantenimiento planeado de máquinas virtuales en Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Cómo tooschedule el mantenimiento planeado en máquinas virtuales de Azure](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Actualizaciones de conservación de memoria   
Con esta clase de actualizaciones de Microsoft Azure, las máquinas virtuales en ejecución de los usuarios no se ven afectadas en absoluto. Muchas de estas actualizaciones son toocomponents o servicios que se pueden actualizar sin interferir con hello ejecuta la instancia. Algunas son actualizaciones de la infraestructura de plataforma en sistema operativo del host Hola que pueden aplicarse sin reinicio de hello las máquinas virtuales.

Estas actualizaciones que conservan memoria se realizan con tecnología que permite la migración en vivo local. Cuando se está actualizando, Hola VM se coloca en un *en pausa* estado. Este estado conserva memoria hello en la memoria RAM mientras que recibe de sistema operativo del host subyacente Hola revisiones y actualizaciones necesarias de Hola. Hola VM se reanudará en 30 segundos de pausa. Después de Hola que se reanuda la máquina virtual, su reloj se sincronizará automáticamente.

Debido a período breve pausa de hello, implementar actualizaciones mediante este mecanismo en gran medida reduce el impacto de hello en hello las máquinas virtuales. Sin embargo, no todas las actualizaciones pueden implementarse de esta manera. 

Las actualizaciones de varias instancias (para las máquinas virtuales de un conjunto de disponibilidad) no se aplican a más de un dominio de actualización a la vez.

> [!NOTE]
> Con este método de actualización, las máquinas Linux que tengan versiones anteriores del kernel se ven afectadas por un fallo de kernel. tooavoid este problema, la actualización tookernel versión 3.10.0-327.10.1 o posterior. Para más información, consulte [Una máquina virtual Linux de Azure en un kernel basado en 3.10, envía un pánico después de actualizar el nodo host](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Acciones de reinicio o apagado iniciadas por el usuario
 
Si lleva a cabo un reinicio de hello portal de Azure, Azure PowerShell, interfaz de línea de comandos o restablecer API, puede encontrar eventos Hola Hola [Azure Activity Log](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Si lleva a cabo acción Hola de sistema operativo de la máquina virtual de hello, puede encontrar eventos de hello en los registros de sistema de Hola.

Otros escenarios que suele causar Hola VM tooreboot incluyen varias acciones de cambio de configuración. Normalmente, verá un mensaje de advertencia que indica que está ejecutando una acción determinada se producirá un reinicio de máquina virtual de hello. Algunos ejemplos son las operaciones de cambio de tamaño de VM, cambiar contraseña de hello de la cuenta administrativa de Hola y establecer una dirección IP estática.

### <a name="azure-security-center-and-windows-update"></a>Azure Security Center y Windows Update
Azure Security Center supervisa diariamente las máquinas virtuales Windows y Linux por si faltan actualizaciones del sistema operativo. Security Center recupera una lista de actualizaciones críticas y de seguridad disponibles desde Windows Update o Windows Server Update Services (WSUS), dependiendo de qué servicio está configurado en una máquina virtual Windows. Centro de seguridad también comprueba las actualizaciones más recientes de Hola para sistemas Linux. Si falta una actualización del sistema en la máquina virtual, Security Center le recomienda que aplique las actualizaciones del sistema. aplicación Hello de estas actualizaciones del sistema se controla a través de hello centro de seguridad en hello portal de Azure. Tras la aplicación de algunas actualizaciones, puede ser necesario reiniciar la máquina virtual. Para más información, consulte [Aplicar actualizaciones del sistema en Azure Security Center](../articles/security-center/security-center-apply-system-updates.md).

Como servidores locales, Azure no insertar actualizaciones desde Windows Update tooWindows máquinas virtuales de Azure, ya que estos equipos son previsto toobe administrado por los usuarios. Sin embargo, son recomienda habilitada por la configuración de Windows Update automática de tooleave Hola. Instalación automática de actualizaciones de Windows Update también puede producir reinicios toooccur después de aplican las actualizaciones de Hola. Para más información, consulte [Windows Update: preguntas frecuentes](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Otras situaciones que afectan a la disponibilidad de saludo de la máquina virtual
Hay otros casos en que Azure activamente puede suspender la aplicación de Hola de una máquina virtual. Recibirá notificaciones por correo electrónico antes de que se realiza esta acción, por lo que tendrá una oportunidad tooresolve Hola problemas subyacentes. Las infracciones de seguridad y de expiración de Hola de métodos de pago son ejemplos de problemas que afectan a la disponibilidad de la máquina virtual.

### <a name="host-server-faults"></a>Errores en el servidor host 
Hola VM está hospedado en un servidor físico que se ejecuta dentro de un centro de datos de Azure. Hola servidor físico ejecuta un agente habían llamado hello agente de Host en suma tooa algunos otros componentes de Azure. Cuando estos componentes de software de Azure en el servidor físico de hello dejan de responder, sistema de supervisión de hello desencadena un reinicio Hola host tooattempt de recuperación del servidor. Hola VM está disponible normalmente en cinco minutos y continúa toolive en hello mismo host como anteriormente.

Errores de servidor suelen deberse al error de hardware, por ejemplo, error de Hola de un disco duro o una unidad de estado sólido. Azure continuamente supervisa estas apariciones, identifica los errores subyacentes de Hola e implementa las actualizaciones una vez se ha implementado y probado mitigación Hola.

Porque algunos errores en el servidor host pueden ser el servidor de toothat específico, se puede mejorar una situación de reinicio de máquina virtual repetida por manualmente volver a implementar el servidor de host de hello VM tooanother. Esta operación puede realizarse utilizando hello **volver a implementar** opción de página de detalles de Hola de hello VM o deteniendo y reiniciando Hola VM Hola portal de Azure.

### <a name="auto-recovery"></a>Recuperación automática
Si el servidor de host de hello no se reinicia por alguna razón, Hola plataforma Windows Azure inicia un servidor de recuperación automática acción tootake Hola defectuoso host fuera de la rotación de una investigación más extensa. 

Todas las máquinas virtuales en ese host están en servidor de host diferente, correcto tooa reubicado automáticamente. Este proceso suele tardar menos de 15 minutos. toolearn más información acerca del proceso de recuperación automática de hello, consulte [recuperación automática de máquinas virtuales](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Mantenimiento no planeado
En raras ocasiones, Hola podría necesita tooensure de actividades de mantenimiento de tooperform Hola estado general de la plataforma Windows Azure Hola de equipo de operaciones de Azure. Este comportamiento podría afectar a la disponibilidad de la máquina virtual, y que suele generar Hola misma acción de recuperación automática como se describió anteriormente.  

Reparaciones no planeadas Hola siguientes:

- Desfragmentación urgente de nodos
- Actualizaciones urgentes de los conmutadores de la red

### <a name="vm-crashes"></a>Bloqueos en la máquina virtual
Máquinas virtuales podrían reiniciarse debido a problemas de hello propia máquina virtual. carga de trabajo de Hola o rol que se ejecuta en hello VM puede desencadenar una comprobación de errores dentro de hello sistema operativo. Ayuda a determinar el motivo de Hola de bloqueo de hello, ver los registros de aplicación y del sistema de Hola de máquinas virtuales de Windows y Hola registros serie para las máquinas virtuales de Linux.

### <a name="storage-related-forced-shutdowns"></a>Apagados forzados relacionados con el almacenamiento
Máquinas virtuales en Azure se basan en los discos virtuales para el sistema operativo y el almacenamiento de datos que se hospeda en una infraestructura de almacenamiento de Azure Hola. Cada vez que la disponibilidad de Hola o conectividad entre Hola VM y discos virtuales Hola asociado se vea afectada durante más de 120 segundos, Hola plataforma Windows Azure realiza un cierre forzado de hello las máquinas virtuales tooavoid daños en los datos. Hola las máquinas virtuales están encendidas automáticamente a una vez restaurada la conectividad de almacenamiento. 

Hola del cierre de hello puede sea lo más corta cinco minutos pero puede ser mucho mayores. siguiente Hello es uno de los casos concretos de Hola que está asociado a cierres forzados relativas al almacenamiento: 

**Superación de los límites de E/S**

Máquinas virtuales podrían temporalmente apagarse cuando las solicitudes de E/S constantemente se acelera porque el volumen de Hola de operaciones de E/S por segundo (IOPS) supera el límite de hello E/S de disco de Hola. (Almacenamiento en disco estándar se limita too500 e/s por segundo.) toomitigate este problema, utilice la creación de bandas en disco o configurar el espacio de almacenamiento de hello dentro de hello invitados de máquinas virtuales, dependiendo de la carga de trabajo de Hola. Para más información, consulte [Configuring Azure Virtual Machines for Optimal Storage Performance](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx) (Configuración de máquinas virtuales de Azure para que el rendimiento del almacenamiento sea óptimo).

Límites de IOPS superior están disponibles a través de almacenamiento de Azure Premium con seguridad too80, IOPS 000. Para más información, consulte el artículo sobre [Premium Storage de alto rendimiento](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Otros incidentes
En circunstancias excepcionales, un problema muy generalizado puede afectar a varios servidores de un centro de datos de Azure. Si se produce este problema, Hola, equipo de Azure envía correo electrónico las suscripciones de notificaciones toohello afectado. Puede comprobar hello [panel de estado del servicio Azure](https://azure.microsoft.com/status/) y Hola portal de Azure para estado de Hola de interrupciones en curso y más allá de los incidentes.
