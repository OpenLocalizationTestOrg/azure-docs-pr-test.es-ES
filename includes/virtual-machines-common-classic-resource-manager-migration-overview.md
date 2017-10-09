# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos
En este artículo se describe cómo permitimos el acceso a la migración de infraestructura como un recurso de servicio (IaaS) de modelos de implementación de hello clásico tooResource Manager. Se puede leer más información sobre [características y ventajas de Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md). Se detalla cómo tooconnect recursos de dos modelos de implementación de Hola que coexistan en su suscripción mediante el uso de virtual puertas de enlace de sitio a sitio de red.

## <a name="goal-for-migration"></a>Objetivo para la migración
Resource Manager permite implementar aplicaciones complejas a través de plantillas, configura las máquinas virtuales mediante extensiones de máquina virtual e incorpora la administración de acceso y el etiquetado. Azure Resource Manager incluye una implementación escalable en paralelo para máquinas virtuales en conjuntos de disponibilidad. nuevo modelo de implementación de Hello también proporciona administración de ciclo de vida de proceso, red y almacenamiento por separado. Por último, nos centramos en habilitar la seguridad de forma predeterminada con la aplicación hello de máquinas virtuales en una red virtual.

Casi todas las características de Hola de modelo de implementación clásica de Hola se admiten para el proceso, red y almacenamiento en el Administrador de recursos de Azure. toobenefit de nuevas capacidades de hello en el Administrador de recursos de Azure, puede migrar las implementaciones de modelo de implementación de hello clásico.

## <a name="supported-resources-for-migration"></a>Recursos que se admiten en la migración
Estos recursos de IaaS clásicos se admiten durante la migración

* Máquinas virtuales
* Conjuntos de disponibilidad
* Cloud Services
* Cuentas de almacenamiento
* Redes virtuales
* Puertas de enlace de VPN
* Express puertas de enlace de ruta _(Hola misma suscripción que la red Virtual solo)_
* Grupos de seguridad de red 
* Tablas de ruta 
* Direcciones IP reservadas 

## <a name="supported-scopes-of-migration"></a>Ámbitos admitidos de la migración
Hay 4 maneras diferentes de migración de toocomplete de recursos de proceso, red y almacenamiento. Dichas maneras son 

* Migración de máquinas virtuales (NO en una red virtual)
* Migración de máquinas virtuales (en una red virtual)
* Migración de cuentas de almacenamiento
* Recursos sin conectar (grupos de seguridad de red, tablas de ruta e IP reservadas)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migración de máquinas virtuales (NO en una red virtual)
En el modelo de implementación del Administrador de recursos de hello, seguridad es obligatorio para las aplicaciones de forma predeterminada. Todas las máquinas virtuales deben toobe en una red virtual en el modelo de administrador de recursos de Hola. Hola reinicios de la plataforma Windows Azure (`Stop`, `Deallocate`, y `Start`) Hola máquinas virtuales como parte de la migración de Hola. Tiene dos opciones para redes virtuales Hola Hola máquinas virtuales se migrará a:

* Puede solicitar Hola plataforma toocreate una nueva red virtual y migrar la máquina virtual en hello en la nueva red virtual de Hola.
* Puede migrar la máquina virtual de hello en una red virtual existente en el Administrador de recursos.

> [!NOTE]
> En este ámbito de la migración, ambos Hola operaciones de plano de administración y operaciones de datos plano hello no pueden permitirse durante un período de tiempo durante la migración de Hola.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migración de máquinas virtuales (en una red virtual)
Para la mayoría de las configuraciones de máquina virtual, solo los metadatos de hello está migrando entre los modelos de implementación de hello clásico y Administrador de recursos. Hola subyacentes de las máquinas virtuales se ejecutan en hello mismo hardware, Hola igual de red y con Hola mismo almacenamiento. las operaciones de administración plano Hello no pueden permitirse durante un período determinado de tiempo durante la migración de Hola. Sin embargo, el plano de datos de hello continúa toowork. Es decir, las aplicaciones que se ejecutan en máquinas virtuales (clásicas) no provocará un tiempo de inactividad durante la migración de Hola.

Hola siguiendo configuraciones no se admite actualmente. Si se agrega compatibilidad con futuras hello, algunas máquinas virtuales en esta configuración podrían suponer un tiempo de inactividad (vaya a través de detención, Cancelar y reiniciar las operaciones de máquina virtual).

* Tiene más de un conjunto de disponibilidad en un único servicio en la nube.
* Tiene uno o varios conjuntos de disponibilidad y máquinas virtuales que no están en un conjunto de disponibilidad en un único servicio en la nube.

> [!NOTE]
> En este ámbito de la migración, no puede permitirse plano de administración de Hola durante un período de tiempo durante la migración de Hola. Para determinadas configuraciones descritas anteriormente, se producirá un tiempo de inactividad en el plano de datos.
>
>

### <a name="storage-accounts-migration"></a>Migración de cuentas de almacenamiento
tooallow una migración sin problemas, puede implementar máquinas virtuales del Administrador de recursos en una cuenta de almacenamiento clásico. Con esta funcionalidad, los recursos de procesos y redes se pueden y se deben migrar con independencia de las cuentas de almacenamiento. Cuando haya migrado a través de las máquinas virtuales y red Virtual, necesitará toomigrate sobre el proceso de migración de almacenamiento cuentas toocomplete Hola.

> [!NOTE]
> modelo de implementación del Administrador de recursos de Hello no tiene el concepto de Hola de clásico imágenes y discos. Cuando cuenta de almacenamiento de hello es migradas, clásicas imágenes y discos no están visibles en la pila del Administrador de recursos de hello pero Hola realizar una copia de discos duros virtuales permanecen en la cuenta de almacenamiento de Hola.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Recursos sin conectar (grupos de seguridad de red, tablas de ruta e IP reservadas)
Grupos de seguridad de red, tablas de rutas y direcciones IP reservadas que no están conectados tooany máquinas virtuales y redes virtuales se pueden migrar de forma independiente.

<br>

## <a name="unsupported-features-and-configurations"></a>Configuraciones y características no admitidas
Actualmente, no se admiten determinadas características y configuraciones. Hola siguientes secciones describe los nuestras recomendaciones alrededor de ellos.

### <a name="unsupported-features"></a>Características no admitidas
Hola siguientes características no se admite actualmente. Puede la posibilidad de quitar esta configuración, migrar máquinas virtuales de hello y, a continuación, volver a habilitar la configuración de hello en el modelo de implementación del Administrador de recursos de Hola.

| Proveedor de recursos | Característica | Recomendación |
| --- | --- | --- |
| Proceso |Discos de máquinas virtuales no asociados. | obtener migrará blobs de disco duro virtual de Hello detrás de estos discos cuando se migra Hola cuenta de almacenamiento |
| Proceso |Imágenes de máquina virtual. | obtener migrará blobs de disco duro virtual de Hello detrás de estos discos cuando se migra Hola cuenta de almacenamiento |
| Red |ACL de puntos de conexión. | Quitar las ACL de los puntos de conexión y vuelva a intentar la migración. |
| Red |Red virtual con ExpressRoute Gateway y VPN Gateway  | Quitar Hola puerta de enlace VPN antes de comenzar la migración y, a continuación, vuelva a crear Hola puerta de enlace VPN una vez completada la migración. Más información acerca de la [migración de ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Red |ExpressRoute con vínculos de autorización  | Quitar conexión de red de hello ExpressRoute circuito toovirtaul antes de comenzar la migración y, a continuación, vuelva a crear conexión Hola una vez completada la migración. Más información acerca de la [migración de ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Red |Application Gateway | Quitar Hola puerta de enlace de aplicaciones antes de comenzar la migración y, a continuación, vuelva a crear Hola puerta de enlace de aplicaciones una vez completada la migración. |
| Red |Redes virtuales que usan el emparejamiento de VNET. | Migrar la red Virtual tooResource Manager y, a continuación, del mismo nivel. Más información acerca del [emparejamiento de VNET](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Configuraciones no admitidas
Hola siguiendo configuraciones no se admite actualmente.

| Servicio | Configuración | Recomendación |
| --- | --- | --- |
| Resource Manager |Control de acceso basado en rol para recursos clásicos |Porque Hola URI de los recursos de hello es modificado después de la migración, se recomienda que planee las actualizaciones de directiva RBAC Hola que necesitan toohappen después de la migración. |
| Proceso |Varias subredes asociadas con una máquina virtual |Actualizar Hola subred configuración tooreference solo subredes. |
| Proceso |Máquinas virtuales que pertenecen tooa de red virtual, pero no tiene una subred explícita asignada |Si lo desea, puede eliminar Hola máquina virtual. |
| Proceso |Máquinas virtuales que tienen alertas, directivas de escalado automático |migración de Hello lleva a cabo y se quitan estas opciones. Se recomienda evaluar su entorno antes de Hola migración. Como alternativa, puede volver a configurar configuración de alertas de hello una vez completada la migración. |
| Proceso |Extensiones XML de máquina virtual (BGInfo 1.*, depurador de Visual Studio, Web Deploy y depuración remota) |ya que no es compatible. Se recomienda que quite estas extensiones de la migración de toocontinue de máquina virtual de Hola o se quitan automáticamente durante el proceso de migración de Hola. |
| Proceso |Diagnóstico de arranque con Almacenamiento premium |Deshabilitar la característica de diagnóstico de arranque para hello las máquinas virtuales antes de continuar con la migración. Puede volver a habilitar el diagnóstico de arranque en la pila del Administrador de recursos de hello una vez completada la migración de Hola. Además, se deben eliminar los blobs que se utilizan para los registros de captura de pantalla y de serie, por lo que ya no se cobra por los blobs. |
| Proceso |Servicios en la nube que contienen roles web y de trabajo |Actualmente no se admite. |
| Red |Redes virtuales que contienen máquinas virtuales y roles web y de trabajo |Actualmente no se admite. |
| Servicio de aplicaciones de Azure |Redes virtuales que contienen entornos del Servicio de aplicaciones |Actualmente no se admite. |
| HDInsight de Azure |Redes virtuales que contienen servicios de HDInsight |Actualmente no se admite. |
| Dynamics Lifecycle Services |Redes virtuales que contienen máquinas virtuales administradas por Dynamics Lifecycle Services |Actualmente no se admite. |
| Azure AD Domain Services |Redes virtuales que contienen servicios de dominio de Azure AD |Actualmente no se admite. |
| Azure RemoteApp |Redes virtuales que contienen implementaciones de Azure RemoteApp |Actualmente no se admite. |
| Administración de API de Azure |Redes virtuales que contienen implementaciones de Azure API Management |Actualmente no se admite. Hola toomigrate IaaS VNET, cambie Hola red virtual de hello implementación de administración de API que no es una operación de ningún tiempo de inactividad. |
| Proceso |Extensiones de Azure Security Center con una red virtual que tiene VPN Gateway en conectividad de tránsito o una puerta de enlace de ExpressRoute con servidor DNS local |Centro de seguridad de Azure automáticamente instala las extensiones en su toomonitor de máquinas virtuales de su seguridad y generar alertas. Estas extensiones normalmente se instalan automáticamente si Hola directiva de centro de seguridad de Azure está habilitada en la suscripción de Hola. La migración de la puerta de enlace de ExpressRoute no se admite actualmente y las puertas de enlace de VPN con conectividad de tránsito pierde el acceso local. Eliminación ExpressRoute puerta de enlace o migrar puerta de enlace VPN con conectividad de tránsito hace internet access tooVM almacenamiento cuenta toobe perdido cuando para continuar con la confirmación de migración de Hola. migración de Hello no continuará cuando esto sucede porque no se pueden rellenar blob del estado de agente de invitado de Hola. Se recomienda toodisable directiva de centro de seguridad de Azure en la suscripción de Hola 3 horas antes de continuar con la migración. |

