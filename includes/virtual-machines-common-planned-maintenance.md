Azure lleva a cabo periódicamente actualizaciones tooimprove Hola confiabilidad, el rendimiento y seguridad de infraestructura de host de Hola para máquinas virtuales. Estas actualizaciones oscilar entre componentes de software de hello entorno (por ejemplo, sistema operativo, hipervisor y diversos agentes implementados en el host de hello), host de aplicación de revisiones actualizar componentes de red, toohardware retirada. mayoría de Hola de estas actualizaciones se realizan sin ninguna máquina virtual de toohello hospedado de impacto. Sin embargo, hay casos en los que las actualizaciones tienen un impacto:

- Si el mantenimiento de hello no requiere un reinicio, Azure usa Hola de migración en contexto toopause VM mientras se actualiza el host de Hola.

- Si mantenimiento requiere un reinicio, recibirá un aviso de cuando Hola mantenimiento está planeado. En estos casos, se deberá también se puede asignar un período de tiempo donde puede empezar a mantenimiento Hola usted mismo, cada vez que se adapte a sus necesidades.

En esta página se describe cómo Microsoft Azure realiza ambos tipos de mantenimiento. Para obtener más información acerca de eventos no planeados (interrupciones), vea Administrar disponibilidad de Hola de máquinas virtuales para [Windows] (.. / articles/virtual-machines/windows/manage-availability.md) o [Linux](../articles/virtual-machines/linux/manage-availability.md).

Hola de aplicaciones que se ejecutan en una máquina virtual puede recopilan información acerca de las próximas actualizaciones a través de servicio de metadatos de Azure [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) o [Linux] (.. / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Migración de máquina virtual en contexto

Cuando no es necesario reiniciar después de una actualización, se usa una migración en vivo en contexto. Durante la actualización de Hola Hola virtual machine se pausa durante unos 30 segundos, conservar memoria hello en la RAM, mientras Hola entorno de hospedaje aplica revisiones y actualizaciones necesarias de Hola. a continuación, se reanuda la máquina virtual de Hola y reloj Hola de máquina virtual de Hola se sincroniza automáticamente.

En las máquinas virtuales de conjuntos de disponibilidad, los dominios de actualización se actualizan de uno en uno. Todas las máquinas virtuales en un dominio de actualización (UD) están en pausa, actualizar y, a continuación, reanudar antes de que pase el mantenimiento planeado en toohello UD siguiente.

Algunas aplicaciones pueden resultar afectadas por estos tipos de actualizaciones. Las aplicaciones que realizan el procesamiento, como medios de transmisión por secuencias o transcodificación o escenarios, de red de alto rendimiento de eventos en tiempo real no estén diseñada tootolerate una pausa de segundo 30. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Mantenimiento que requiere un reinicio

Cuando las máquinas virtuales necesitan toobe reinicia para el mantenimiento planeado, se le notifica de antemano. Mantenimiento planeado tiene dos fases: Hola ventana autoservicio y una ventana de mantenimiento programado.

Hola **ventana autoservicio** le permite iniciar el mantenimiento de hello en las máquinas virtuales. Durante este tiempo, puede consultar su estado de cada toosee de máquina virtual y comprobar el resultado de hello de la última solicitud de mantenimiento.

Cuando se inicia el mantenimiento de autoservicio, la máquina virtual está tooa movida nodo que ya se ha actualizado y, a continuación, enciende. Dado que Hola VM que se reinicie, disco temporal de Hola se pierde y direcciones IP dinámicas asociadas con la interfaz de red virtual se actualizan.

Si empieza mantenimiento de autoservicio y hay un error durante el proceso de hello, se detiene la operación de hello, hello no se actualiza la máquina virtual y también se quita del iteración de mantenimiento de hello planeada. Se había conectado en un momento posterior a una nueva programación y se ofrecen nuevas oportunidades toodo autoservicio mantenimiento. 

Cuando ha transcurrido la ventana de autoservicio de hello, Hola **ventana de mantenimiento programada** comienza. Durante este período de tiempo, puede consultar para la ventana de mantenimiento de hello, pero ya no estará toostart capaz de mantenimiento de Hola.

## <a name="availability-considerations-during-planned-maintenance"></a>Consideraciones sobre disponibilidad durante el mantenimiento planeado 

Si decide toowait hasta Hola planeada ventana de mantenimiento, hay algunos tooconsider cosas para mantener Hola mayor disponibilidad de las máquinas virtuales. 

### <a name="paired-regions"></a>Regiones emparejadas

Cada región de Azure se empareja con otra región dentro de hello mismo geography, realizan un par regional junto. Durante el mantenimiento planeado, Azure solo actualizará hello las máquinas virtuales en una única región de un par de región. Por ejemplo, al actualizar Hola máquinas virtuales en Ee.uu. Central Norte, Azure no actualizará las máquinas virtuales de Ee.uu. Central sur en hello mismo tiempo. Sin embargo, otras regiones como Europa del Norte puede estar en proceso de mantenimiento en Hola mismo tiempo como UU. Comprender cómo funcionan los pares de regiones puede ayudar a distribuir mejor las máquinas virtuales entre regiones. Para más información, consulte [Regiones de Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Conjuntos de disponibilidad y conjuntos de escalado

Al implementar una carga de trabajo en máquinas virtuales de Azure, puede crear máquinas virtuales de hello dentro de una aplicación de tooyour disponibilidad conjunto tooprovide alta disponibilidad. Esto garantiza que durante un corte de suministro o un evento de mantenimiento, al menos haya una máquina virtual disponible.

Dentro de un conjunto de disponibilidad, máquinas virtuales individuales se reparten entre los dominios de actualización de too20 (ud). Durante el mantenimiento planeado, solo un dominio de actualización se ve afectado en un momento dado. Tenga en cuenta que orden Hola de dominios de actualización que se ve afectado no siempre ocurren secuencialmente. 

Conjuntos de escalas de máquina virtual son un recurso de proceso de Azure que le permite toodeploy y administración un conjunto de máquinas virtuales idénticos como un único recurso. conjunto de escalas de Hola se implementa automáticamente entre dominios de actualización, como las máquinas virtuales en un conjunto de disponibilidad. Igual que con los conjuntos de disponibilidad, con los conjuntos de escalado solo un dominio de actualización dado resulta afectado en un momento determinado.

Para obtener más información acerca de cómo configurar las máquinas virtuales de alta disponibilidad, vea la disponibilidad de Hola de administrar las máquinas virtuales de Windows (.. / articles/virtual-machines/windows/manage-availability.md) o [Linux](../articles/virtual-machines/linux/manage-availability.md).
