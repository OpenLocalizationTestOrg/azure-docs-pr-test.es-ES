## <a name="what-are-service-bus-queues"></a>¿Qué son las colas del Bus de servicio?
Las colas del Bus de servicio son compatibles con el modelo de comunicación de **mensajería asíncrona** . Cuando se usan colas, los componentes de una aplicación distribuida no se comunican directamente entre sí, sino que intercambian mensajes a través de una cola, que actúa como un intermediario (agente). Un productor de mensajes (remitente) entrega una cola de toohello de mensajes y, a continuación, continúa su procesamiento. De forma asincrónica, un consumidor de mensaje (receptor) extrae los mensajes de Hola de cola de Hola y lo procesa. productor de Hello no tienen toowait una respuesta de consumidor de hello en orden toocontinue tooprocess y enviar más mensajes. Las colas ofrecen **primero en ENTRAR, primero en salir (FIFO)** tooone entrega los mensajes más consumidores en competencia. Es decir, mensajes normalmente se recibe y procesa receptores de hello en orden de hello en el que se agregaron toohello cola, y cada mensaje lo recibe y procesa por un solo consumidor de mensaje.

![QueueConcepts](./media/howto-service-bus-queues/sb-queues-08.png)

Las colas del Bus de servicio son una tecnología de uso general que puede utilizarse en una variedad de escenarios:

* Comunicación entre los roles de trabajo y web en una aplicación de Azure de niveles múltiples.
* Comunicación entre aplicaciones locales y aplicaciones hospedadas de Azure en una solución híbrida.
* Comunicación entre componentes de una aplicación distribuida que se ejecuta en local en distintas organizaciones o departamentos de una organización.

Uso de colas permite tooscale las aplicaciones más fácilmente y habilitar más arquitectura tooyour de resistencia.


