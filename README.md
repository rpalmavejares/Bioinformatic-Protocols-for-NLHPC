# Bioinformatic-Protocols-for-NLHPC
Documentación con Tips y Buenas Practicas para el uso del NLHPC para tareas de Bioinformática y/o similares

## Creación de cuentas, solicitudes de horas de computo, CPUs y Storage.

### Creación de cuentas

La creación de cuentas del NLHPC se puede separar en 2 grupos. 1) Usuarios nuevos sin conexion al NLHPC y 2) Usuarios que seran parte de un grupo ya existente en el NLHPC.

1) En el primer grupo de usuarios, la creación de cuentas se da de forma exclusiva a un/una PI o investigadores jovenes, los cuales deberan rellenar el siguiente formulario con la información correspondiente https://solicitudes.nlhpc.cl/.

2) En el caso de que el PI este generando una cuenta para su grupo o equipoy que requiera mas de 1 cuenta, lo ideal es generar 1 cuenta de PI en https://solicitudes.nlhpc.cl/ y cuentas individuales para cada miembro del grupo, es decir.
```
   a) 1 Cuenta de PI.
   b) N Cuentas, 1 por cada miembro del Team.
 ```  
La recomendación principal de la creación de cuentas para un grupo es idealmente, asignar un Nombre del Team Investigación. Como ejemplo: CRG-LAB1, CRG_UOH o, en mi caso particular, Mathomics.
Esto facilitara luego, la creación de cuentas para miembros del mismo grupo, y la asignación de permisos, protocolos y tools que el grupo completo necesitara eventualmente.

La recomendación principal es que cada nueva cuenta sea creada o solicitada por 1 solo miembro de cada Team o Grupo. Esta tarea puede recaer directamente al PI o puede ser un encargado seleccionado.

Para mantener el orden y la trazabilidad de los datos, lo ideal es que cada usuario pueda acceder a 1 sola cuenta. Compartir claves incurre una alta probabilidad de accesos no autorizados, uso de recursos no controlados o eliminación de datos sin consentimiento.
En el caso de necesitar una cuenta de datos la cual sera utilizada solo por periodos cortos de tiempo, con varios usuarios distintos, se recomienda crear una cuenta especial de invitado. Esta cuenta debe estar registrada con el mismo PI y bajo el mismo Team.
Por lo general estas cuentas se usan solo para compartir datos con otros investigadores, o estudiantes en practica, los cuales no necesitan cuentas permanentes individuales.


### Solicitudes de horas de computo, CPUs y storage.

Durante la creación de cuentas de cuentas del PI, se requerira establecer una cuota de horas de computo. Esta solicitud se asignara como limite de ejecución de tareas con una duración de 1 año, a partir de la fecha de la primera solicitud. Estas horas de computo se estableceran como limite para cada Team, por lo que no es necesario generar una peticion de horas de computo por cada cuenta. 

En el caso que las horas de computo se cumplan, ninguna cuenta del Team podra seguir ejecutando tareas, hasta generar una nueva solicitud en https://solicitudes.nlhpc.cl/.
Por lo general, una solicitud de horas de computo debera tomar en cuenta la cantidad de miembros, las tareas que se necesitan ejecutar, la cantidad de veces que se necesita ejecutar la misma tarea. 
Como un buen estimador en bioinformática, la cantidad de horas para limpiar, ensamblar, anotar y analizar genomas durante 1 año calendario es de entre 20.000 y 50.000 horas por cuenta.

En el caso de cuentas con gran volumen de datos y varos analisis al año, las horas por cuenta pueden superar facilmente los 250.000 horas de computo.
La recomendación es: Para Teams nuevos: entre 10.000 a 15.000 horas de computo por cuenta. Para Teams con experiencia, entre 50.000 a 70.000 horas de computo por cuenta.

En el caso de que la cantidad de horas de computo solicitadas sea muy por debajo de lo necesario por cada Team, el equipo de Soporte del NLHPC enviara un correo a cada cuenta con la notificación de que el numero de horas esta por acabarse o completamente utilizada. En esta notificación, cada cuenta tendra desglozado el numero de horas que se utilizaron. 

Para no repetir una nueva solicitud de horas de computo cada 4 o 6 meses, lo ideal es utilizar la información obtenida en la notificación del NLHPC y reajustar la petición para que coincida con el periodo de 12 meses.

#### El cobro de horas de computo se realiza sobre el uso real, y no sobre las horas solicitadas en la creación de cuentas. ####

### CPUs y Storage

Al crear una nueva cuenta en el NLHPC, si no se especifican la cantidad de recursos de CPU y Storage, cada cuenta tendra por default 88 CPU y 120Gb de Storage. En el caso de las CPUs significa que el usuario, puede utilizar como máximo 88 CPUs al mismo tiempo durante procesos de ejecución, es decir, si ejecutamos 3 procesos con 40 CPU cada 1.

      a) Proceso 1 con 40 CPU. Este proceso se ejecutara sin problemas, siempre y cuando existan recursos en el NLHPC. 
      b) Proceso 2 con 40 CPU. Este proceso se ejecutara sin problemas, siempre y cuando existan recursos en el NLHPC.
      c) Proceso 3 con 40 CPU. Este proceso no se podra ejecutar hasta que el proceso a) o b) terminen. 

En el caso del Storage, este valor es el limite maximo con el cual podremos guardar nuestros archivos o tareas. Si se da la instancia de que nuestra cuota de Storage esta en su limite, no se podran seguir ejecutando tareas, aun teniendo CPUs y horas de computo disponible. 
En el caso de que lleguemos al limite del Storage, durante la ejecución de una de nuestras tareas, esta terminara antes forzosamente, y se notificara al usuario de la falta de espacio en nuestra cuenta.

#### Tanto la cantidad de CPUs como el Storage se pueden solicitar de forma indivual para para cuenta/usuario, por lo que es necesario revisar los requerimientos de cada uno ####

A modo general. el uso de 100 CPUs y 500Gb para Team nuevos y 350+ CPUs y 1TB+ de Storage para Teams antiguos es recomendable.







