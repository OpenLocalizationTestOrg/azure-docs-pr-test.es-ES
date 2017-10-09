
* conversión de Hello requiere un reinicio de hello VM, por lo que programar migración de Hola de las máquinas virtuales durante un período de mantenimiento existente. 

* Hola conversión no es reversible. 

* Estar seguro de conversión de hello tootest. Migrar una máquina virtual de prueba antes de realizar la migración de hello en producción.

* Durante la conversión de hello, cancela la asignación Hola máquina virtual. Hola VM recibe una nueva dirección IP cuando se inicia después de la conversión de Hola. Si es necesario, puede [asignar una dirección IP estática](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello máquina virtual.

* Hello VHD originales y cuenta de almacenamiento de hello usada por hello VM antes de la conversión no se eliminan. Se siguen tooincur cargos. tooavoid cobrándole para estos artefactos, eliminar los blobs de disco duro virtual originales de hello después de comprobar que la conversión de hello está completa.
