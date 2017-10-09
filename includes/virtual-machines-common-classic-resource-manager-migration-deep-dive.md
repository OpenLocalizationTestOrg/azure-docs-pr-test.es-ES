## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Significado de la migración de los recursos de IaaS de tooResource de modelo de implementación clásica de hello Manager
Antes de que se profundizar en los detalles de hello, echemos un vistazo a diferencia de hello entre operaciones de datos plano y plano de administración en los recursos de IaaS de Hola.

* *Plano de Control y administración* describe llamadas de Hola que entran en el plano de control y administración de Hola u Hola API para la modificación de los recursos. Por ejemplo, operaciones, como crear una máquina virtual, reiniciar una máquina virtual y la actualización de una red virtual con una nueva subred administran Hola ejecuta recursos. No afectan directamente a instancias de conexión toohello.
* *Plano de datos* (aplicación) describe hello en tiempo de ejecución de la propia aplicación hello e implica la interacción con instancias que no recorren Hola API de Azure. Por ejemplo, el acceso a su sitio web o la extracción de datos desde una instancia de SQL Server o un servidor MongoDB en ejecución se consideran interacciones de aplicación o en el plano de datos. Copiar un blob de una cuenta de almacenamiento y tener acceso a un público tooRDP de dirección IP o SSH en la máquina virtual de hello también son plano de datos. Estas operaciones mantendrán aplicación Hola que se ejecuta en proceso, red y almacenamiento.

Entre bastidores de hello, plano de datos de hello es Hola mismo entre Hola modelo de implementación clásica y pila del Administrador de recursos. Durante el proceso de migración, se traduzca representación Hola de recursos de Hola de modelo de implementación de hello clásico toothat en pila del Administrador de recursos de Hola. Como resultado, deberá toouse nuevas herramientas, API, SDK toomanage los recursos en la pila del Administrador de recursos de Hola.

![Captura de pantalla que muestra la diferencia entre el plano de administración o control, y el plano de datos](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> En algunos escenarios de migración, Hola plataforma Windows Azure detiene, desasigna y reinicia las máquinas virtuales. Esto provoca un corto período de inactividad en el plano de datos.
>

## <a name="hello-migration-experience"></a>experiencia de migración de Hola
Antes de empezar la experiencia de migración de hello, se recomienda siguiente hello:

* Asegúrese de que los recursos de Hola que desea toomigrate no usar las características no admitidas o configuraciones. Normalmente plataforma Hola detecta estos problemas y genera un error.
* Si tiene máquinas virtuales que no están en una red virtual, se detiene y se cancela la asignación como parte del programa Hola a preparar la operación. Si no desea que la dirección IP pública de toolose hello, visión la reserva de dirección IP de hello antes de desencadenar Hola preparar la operación. Sin embargo, si hello las máquinas virtuales están en una red virtual, no se detiene y cancela la asignación de.
* Planear la migración durante el horario no comercial tooaccommodate errores inesperados que pueden suceder durante la migración.
* Descargar configuración actual de Hola de las máquinas virtuales con PowerShell, comandos de la interfaz de línea de comandos (CLI) o toomake de las API de REST, facilitando la validación después de paso de preparación de hello es completa.
* Actualizar el modelo de implementación de administrador de recursos de automatización/puesta en marcha las secuencias de comandos toohandle Hola antes de iniciar la migración de Hola. Opcionalmente, puede realizar las operaciones GET cuando hay recursos de Hola Hola preparado estado.
* Evaluar las directivas RBAC de Hola que se configuran en los recursos clásicos de IaaS de Hola y plan una vez completada la migración de Hola.

flujo de trabajo de migración de Hello es como se indica a continuación.

![Captura de pantalla que muestra el flujo de trabajo de migración de Hola](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Todas las operaciones de Hola que se describe en las secciones siguientes de hello son idempotentes. Si tiene un problema que no sea una característica no compatible o un error de configuración, se recomienda que vuelva a intentar Hola preparar, anular o confirmar la operación. Hola plataforma Windows Azure intenta realizar acción Hola de nuevo.
>
>

### <a name="validate"></a>Validación
Hola validar la operación es Hola primer paso en el proceso de migración de Hola. objetivo de Hola de este paso es estado de hello tooanalyze de recursos de hello desea toomigrate en el modelo de implementación clásica de Hola y devolver correcto o con errores si hay recursos de hello capaces de migración.

Selecciona red virtual de Hola o un servicio de nube (si no está en una red virtual) que desea toovalidate para la migración.

* Si Hola recurso no es capaz de migración, Hola plataforma Windows Azure enumera todos los motivos de Hola para ¿por qué no se admite para la migración.

#### <a name="checks-not-done-in-validate"></a>Comprobaciones no realizadas en la validación

Validar operación solo analiza estado Hola de recursos de hello en el modelo de implementación clásica de Hola. Puede comprobar para todos los errores y escenarios no admitidos debido a la configuración de toovarious en el modelo de implementación clásica de Hola. No es posible toocheck para todos los problemas que hello Azure Resource Manager pila puede imponer en recursos de Hola durante la migración. Estos problemas sólo se comprueban cuando recursos Hola someterse a la transformación en el paso siguiente de saludo de la migración, es decir, preparación. tabla de Hello siguiente muestra todos los problemas de hello no se comprueban en validar.


|Comprobaciones de red que no se realizan en la validación|
|-|
|Si una red virtual tiene puertas de enlace de ER y de VPN|
|Conexión de la puerta de enlace de red virtual en estado de desconexión|
|Todos los circuitos ER son pila del Administrador de recursos de tooAzure migrados previamente|
|Comprobaciones de cuota de Azure Resource Manager de los recursos de red, es decir, la IP pública estática, las IP públicas dinámicas, el equilibrador de carga, los grupos de seguridad de red, las tablas de enrutamiento o las interfaces de red |
| Comprobación de que todas las reglas del equilibrador de carga son válidas entre implementaciones y redes virtuales |
| Busque en conflicto de direcciones IP privada entre máquinas virtuales detenido desasignado Hola misma red virtual |

### <a name="prepare"></a>Preparación
Hola preparar la operación es Hola segundo paso en el proceso de migración de Hola. objetivo Hola de este paso es transformación de hello toosimulate de hello recursos de IaaS de recursos del Administrador de tooResource de modelo de implementación clásica y presentar esto en paralelo automáticamente toovisualize.

> [!NOTE] 
> Los recursos del modelo clásico no se modifican durante este paso. Por lo que es un toorun paso seguro si está tratando de salida de migración. 

Seleccionar Hola Hola o red en la nube servicio virtual (si no es una red virtual) que desea tooprepare para la migración.

* Si Hola recurso no es capaz de migración, Hola plataforma Windows Azure detiene el proceso de migración de Hola y enumera motivo Hola ¿por qué Hola preparar error en la operación.
* Si el recurso de hello es capaz de migración, Hola plataforma Windows Azure primera bloquean las operaciones de plano de la administración de Hola para recursos de saludo se está migrando. Por ejemplo, no es capaz de tooadd tooa de disco de datos máquina virtual se está migrando.

Hello plataforma Windows Azure, a continuación, inicia Hola migración de metadatos de implementación clásica modelo tooResource Manager para hello migrar recursos.

Después de preparar Hola operación es completa, tiene la opción de Hola para visualizar los recursos de hello en el modelo de implementación clásica y Administrador de recursos. Para cada servicio de nube en el modelo de implementación clásica de hello, hello plataforma Windows Azure crea un nombre de grupo de recursos que tiene el patrón de hello `cloud-service-name>-Migrated`.

> [!NOTE]
> No es posible tooselect Hola nombre del grupo de recursos que se creó para los recursos migrados (es decir, "-migrado"), pero una vez completada la migración, puede usar Azure Resource Manager movimiento característica toomove recursos tooany grupo de recursos que desee. más información acerca de esta, consulte tooread [Mover grupo de recursos de toonew de recursos o suscripción](../articles/resource-group-move-resources.md)

Estas son dos pantallas para mostrar el resultado de hello después una correcta operación de preparación. Primera pantalla muestra un grupo de recursos que contiene el servicio de nube de hello original. Segunda pantalla muestra hello nuevo "-migrado" grupo de recursos que contiene recursos de Azure Resource Manager equivalentes Hola.

![Captura de pantalla que muestra el servicio en la nube clásico de Portal](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Captura de pantalla que muestra los recursos de Azure Resource Manager del portal en la preparación](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Este es un vistazo entre bastidores de los recursos después de la finalización de saludo de la fase de preparación. Tenga en cuenta que el recurso de hello es plano de datos de hello es Hola mismo. Se representa en el plano de administración de hello (modelo de implementación clásica) y plano de control de hello (Administrador de recursos).

![Entre bastidores de hello en la fase de preparación](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Las máquinas virtuales que no se encuentran en una red virtual clásica se detienen (desasignan) en esta fase de la migración.
>

### <a name="check-manual-or-scripted"></a>Comprobación (manual o mediante scripts)
En el paso de verificación de hello, también puede usar configuración de Hola que descargó toovalidate anterior que la migración de hello está correcto. Como alternativa, puede iniciar sesión en toohello portal y terreno Hola propiedades y recursos toovalidate que la migración de metadatos es correcto.

Si están migrando una red virtual, no se reinicia la mayoría de la configuración de las máquinas virtuales. Para las aplicaciones en esas máquinas virtuales, puede validar que la aplicación hello está todavía activa y en funcionamiento.

Puede probar la supervisión y automatización y los scripts operacionales toosee cuando hello las máquinas virtuales estén funcionando según lo previsto y si las secuencias de comandos actualizadas funcionan correctamente. Operaciones GET sola se admiten cuando hay recursos de Hola Hola preparado estado.

No hay ninguna ventana de tiempo del conjunto antes de que se necesita una migración hello toocommit. Puede mantenerse el tiempo que desee en este estado. Sin embargo, plano de administración de hello está bloqueado para estos recursos hasta que se anule o confirmar.

Si ve algún problema, siempre puede anular la migración de Hola y volver al modelo de implementación clásica de toohello. Después de volver atrás, Hola plataforma Windows Azure, abrirá operaciones de plano de la administración de hello en los recursos de Hola por lo que puede reanudar las operaciones normales en esas máquinas virtuales en el modelo de implementación clásica de Hola.

### <a name="abort"></a>Anulación
Anulación es un paso opcional que puede utilizar toorevert su modelo de implementación clásica de toohello de cambios y detener la migración de Hola. Esta operación elimina Hola metadatos de administrador de recursos para los recursos que se creó en el paso de preparación de hello anterior. 

![Entre bastidores de hello en la fase de anulación](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Esta operación no se puede ejecutar una vez que se desencadena la operación de confirmación Hola.     
>

### <a name="commit"></a>Confirmación
Cuando termine de validación de hello, puede confirmar la migración de Hola. Recursos ya no aparecerá en el modelo de implementación clásica y solo están disponibles en el modelo de implementación de hello Administrador de recursos. Hello recursos migrados se pueden administrar solo en el nuevo portal de Hola.

> [!NOTE]
> Se trata de una operación idempotente. Si se produce un error, se recomienda que vuelva a intentar la operación de Hola. Si continúa toofail, cree una incidencia de soporte técnico o cree un foro post con una etiqueta ClassicIaaSMigration en nuestra [foro de la máquina virtual](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Entre bastidores de hello en la fase de confirmación](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>¿Donde toobegin migración?

Este es un diagrama de flujo que muestra cómo tooproceed con la migración

![Captura de pantalla que muestra los pasos de migración de Hola](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Traducción de los recursos del Administrador de recursos de tooAzure de modelo de implementación clásica
Puede encontrar el modelo de implementación clásica de Hola y representaciones de administrador de recursos de los recursos de hello en hello en la tabla siguiente. Actualmente no se admiten otras funciones y recursos.

| Representación clásica | Representación de Resource Manager | Notas detalladas |
| --- | --- | --- |
| Nombre del servicio en la nube |Nombre DNS |Durante la migración, se crea un nuevo grupo de recursos para cada servicio en la nube con el patrón de nomenclatura de hello `<cloudservicename>-migrated`. Este grupo de recursos contiene todos los recursos. nombre del servicio de nube de Hola se convierte en un nombre DNS que está asociado a la dirección IP pública Hola. |
| Máquina virtual |Máquina virtual |Las propiedades específicas de la máquina virtual se migran sin cambios. Cierta información osProfile, tal como el nombre de equipo, no se almacena en el modelo de implementación clásica de Hola y permanece vacía después de la migración. |
| Recursos de disco adjunto tooVM |TooVM implícita discos conectados |Los discos no se modelan como recursos de nivel superior en el modelo de implementación del Administrador de recursos de Hola. Se migran como discos implícita en hello máquina virtual. Solo los discos que están conectados tooa VM son compatibles actualmente. Máquinas virtuales del Administrador de recursos ahora puede usar cuentas de almacenamiento clásicas, lo que permite Hola discos toobe migra fácilmente sin las actualizaciones. |
| Extensiones de máquina virtual |Extensiones de máquina virtual |Todas las extensiones de recursos de hello, excepto las extensiones XML, se migran desde el modelo de implementación clásica de Hola. |
| Certificados de la máquina virtual |Certificados en Azure Key Vault |Si un servicio de nube contiene certificados de servicio, un nuevo almacén de claves de Azure por cada servicio de nube y mueve los certificados de hello en el almacén de claves de Hola. máquinas virtuales de Hello son tooreference actualizada Hola certificados del almacén de claves de Hola. <br><br> **Nota:** no elimine hello keyvault ya que puede producir hello toogo de máquina virtual en un estado de error. Estamos trabajando en la mejora de cosas en hello back-end para que los almacenes de clave se puede eliminar de forma segura o mueven junto con hello tooa nueva suscripción de máquina virtual. |
| Configuración de WinRM |Configuración de WinRM en osProfile |Se mueve la configuración de administración remota de Windows sin cambios, como parte de la migración de Hola. |
| Propiedad de conjunto de disponibilidad |Recurso de conjunto de disponibilidad | Especificación de conjunto de disponibilidad era una propiedad en hello VM en el modelo de implementación clásica de Hola. Conjuntos de disponibilidad se convierten en un recurso de nivel superior como parte de la migración de Hola. Hello siguientes no se admiten configuraciones: varios conjuntos de disponibilidad por cada servicio de nube o disponibilidad de uno o más conjuntos junto con las máquinas virtuales que no están en ningún conjunto de disponibilidad en un servicio de nube. |
| Configuración de red en una máquina virtual |Interfaz de red principal |Configuración de red en una máquina virtual se representa como recurso de interfaz de red principal de hello después de la migración. Para las máquinas virtuales que no están en una red virtual, la dirección IP interna de hello cambia durante la migración. |
| Varias interfaces de red en una máquina virtual |Interfaces de red |Si una máquina virtual tiene varias interfaces de red asociados a él, cada interfaz de red se convierte en un recurso de nivel superior como parte de la migración de hello en el modelo de implementación de administrador de recursos de hello, junto con todas las propiedades de Hola. |
| Conjunto de punto de conexión de carga equilibrada |Equilibrador de carga |En el modelo de implementación clásica de hello, plataforma Hola asigna un equilibrador de carga implícita para cada servicio en la nube. Durante la migración, se crea un nuevo recurso de equilibrador de carga y conjunto de extremos de equilibrio de carga de Hola se convierte en reglas de equilibrador de carga. |
| Reglas NAT de entrada |Reglas NAT de entrada |Extremos de entrada definidos en hello VM son reglas de traducción de direcciones de red de tooinbound convertido en el equilibrador de carga de Hola durante la migración de Hola. |
| Dirección VIP |Dirección IP pública con nombre DNS |dirección IP virtual de Hola se convierte en una dirección IP pública y está asociado con el equilibrador de carga de Hola. Solo se puede migrar una dirección IP virtual si hay un extremo de entrada asignado tooit. |
| Red virtual |Red virtual |red virtual de Hola se migra, con todas sus propiedades, el modelo de implementación del Administrador de recursos de toohello. Se crea un nuevo grupo de recursos con nombre de hello `-migrated`. |
| Direcciones IP reservadas |Dirección IP pública con método de asignación estático |Migrar direcciones IP reservadas asociado con el equilibrador de carga de hello, junto con la migración de Hola de servicio de nube de Hola o una máquina virtual de Hola. Actualmente, no se admite la migración de direcciones IP reservadas no asociadas. |
| Dirección IP pública por máquina virtual |Dirección IP pública con método de asignación dinámico |Hola dirección IP pública asociada Hola que VM se convierte como un recurso de dirección IP público, con toostatic de conjunto de método de asignación de Hola. |
| Grupos de seguridad de red |Grupos de seguridad de red |Grupos de seguridad de red asociados a una subred se clonan como parte del modelo de implementación del Administrador de recursos de hello migración toohello. Hola NSG en el modelo de implementación clásica de hello no se quita durante la migración de Hola. Sin embargo, las operaciones de plano de la administración de Hola para hello NSG se bloquean cuando la migración de hello está en curso. |
| Servidores DNS |Servidores DNS |Servidores DNS asociados a una red virtual u Hola máquinas virtuales se migran como parte de la migración de recursos correspondiente hello, junto con todas las propiedades de Hola. |
| Rutas definidas por el usuario |Rutas definidas por el usuario |Rutas definidas por el usuario asociadas a una subred se clonan como parte del modelo de implementación del Administrador de recursos de hello migración toohello. Hola UDR en el modelo de implementación clásica de hello no se quita durante la migración de Hola. operaciones de plano de la administración de Hola para hello UDR se bloquean cuando la migración de hello está en curso. |
| Propiedad de reenvío de IP en una configuración de red de máquina virtual |Propiedad Hola NIC de reenvío IP |propiedad de reenvío IP Hello en una máquina virtual es propiedad de tooa convertido en la interfaz de red de Hola durante la migración de Hola. |
| Equilibrador de carga con varias IP |Equilibrador de carga con varios recursos de dirección IP pública |Cada dirección IP pública asociada con el equilibrador de carga de hello es el recurso IP público tooa convertido y asociadas con equilibrador de carga de hello después de la migración. |
| Nombres DNS internos en hello VM |Nombres DNS internos en hello NIC |Durante la migración, sufijos DNS internos de Hola para máquinas virtuales de hello son propiedad de solo lectura de tooa migrados denominada "InternalDomainNameSuffix" hello NIC. sufijo de Hello no cambie después de la migración y resolución de la máquina virtual debe continuar toowork como anteriormente. |
| Puerta de enlace de red virtual |Puerta de enlace de red virtual |Las propiedades de puerta de enlace de red virtual se migran sin cambios. Hola VIP asociada Hola puerta de enlace no cambia ninguno. |
| Sitio de red local |Puerta de enlace de red local |Propiedades de sitio de red local son migrados tooa sin cambios nuevo recurso denominado puerta de enlace de red Local. Este representa prefijos de direcciones locales y la dirección IP de la puerta de enlace remota. |
| Referencias de conexiones |Conexión |Las referencias de conectividad entre la puerta de enlace y el sitio de red local en la configuración de red se representan mediante un recurso recién creado denominado Conexión en el administrador de recursos después de la migración. Todas las propiedades de referencia de conectividad en archivos de configuración de red son recurso de conexión copiada toohello sin cambios recién creado. Conectividad de red virtual tooVNet en clásico se logra mediante la creación de dos túneles IPsec toolocal sitios de red que representa Hola redes virtuales. Se trata de conexión tooVnet2Vnet transformado tipo de modelo del Administrador de recursos sin necesidad de puertas de enlace de red local. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Automatización de tooyour de cambios y herramientas después de la migración
Como parte de la migración de los recursos de modelo de implementación del Administrador de recursos de toohello de hello clásico implementación modelo, tiene tooupdate la automatización existente o tooensure de herramientas que sigue toowork después de la migración de Hola.
