Una máquina virtual de Azure admite la conexión de varios discos de datos. Para obtener un rendimiento óptimo, le interesará número de Hola de toolimit de alta tasa de utilización discos adjuntos toohello máquina virtual tooavoid posible limitación. Si todos los discos no se se utilizan muy en hello mismo tiempo, cuenta de almacenamiento de hello puede admitir un mayor número de discos.

* **Para los discos de Azure administrado:** límite del número de discos administrado es regional y también depende de tipo de almacenamiento de Hola. Hola predeterminada y también el límite máximo de hello es 10.000 por suscripción, por región y por tipo de almacenamiento. Por ejemplo, puede crear hasta too10, administrada estándar 000 discos y también 10.000 premium administra discos en una suscripción y en una región. 

    Las instantáneas administrado y las imágenes se cuentan contra Hola que limitar discos administrados.

* **En el caso de cuentas de almacenamiento estándar:** una cuenta de almacenamiento estándar tiene una tasa total máxima de solicitudes de 20 000 E/S por segundo. Hello IOPS totales en todos los discos de máquina virtual en una cuenta de almacenamiento estándar no debe superar este límite.
  
    Puede calcular aproximadamente número Hola de alta tasa de utilización discos compatibles con una cuenta de almacenamiento estándar único basada en el límite de velocidad de solicitudes de Hola. Por ejemplo, para un nivel básico de máquina virtual, Hola número máximo de gran uso discos es aproximadamente 66 (20.000/300 e/s por segundo por disco), y para una VM de nivel estándar, es aproximadamente 40 (20.000/500 IOPS por disco), como se muestra en la siguiente tabla se Hola. 
* **En el caso de cuentas de almacenamiento premium:** una cuenta de almacenamiento premium tiene una capacidad total máxima de proceso de 50 Gbps. capacidad total de Hello en todos los discos de máquina virtual no debe superar este límite.

