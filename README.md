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

A modo general el uso de recursos optimo es alrededor de:

> 100 CPUs y 500Gb para Team nuevos. <br>
> 200+ CPUs y 1Tb+ de Storage para Teams antiguos <br>

## Modo SUDO, Module LOAD e Instalación de software mediante gestor de paquetes.

### Modo SUDO

En el caso de nuestros computadores personales, podremos acceder a la instalación de tareas mediante SUDO o super usuario.
Este metodo de instalación esta restringido para todas las cuentas del NLHPC a exepcion del equipo de soporte, por lo que ninguna herramienta se podra instalar mediante este metodo, es decir, los comandos tales como:

```
sudo install tool
sudo apt install tool
```
NO son validos.
<br>
En el caso de necesitar instalar una tool que requiera especificamente este comando, existen 2 soluciones especificas.

#### A. Instalación local con el codigo fuente. ####

Para la instalación local de nuestra tool, primero necesitaremos el codigo fuente de la herramienta. Por lo general cualquier tool que utilice el comando SUDO, tiene un codigo fuente, el cual se puede descargar desde la pagina web del software o desde github. En nuestro caso, seguiremos el ejemplo de MEME Suite (https://web.mit.edu/meme/current/share/doc/install.html).

```
tar zxf meme_4.11.4.tar.gz
cd meme_4.11.4
./configure --prefix=$HOME/meme --with-url=http://meme-suite.org --enable-build-libxml2 --enable-build-libxslt
make
make test
make instal
```

En el ejemplo anterior, podemos instalar localmente nuestra tool utilizando el comando especifico:
```
--prefix=$HOME/my_carpeta_personal
o
--prefix=/home/my_cuenta/my_carpeta_personal
```

En el caso de que no exista la opción de instalación del codigo fuente, o encontremos errores dentro del proceso, podemos utilizar la opcion B.

#### B. Solicitud de instalación al equipo de Soporte NLHPC ####

Cada vez que necesitemos instalar herramientas que parecen demasiado complicadas o requieren librerias que no podemos encontrar. Lo mejor es realizar una solicitud al equipo de Soporte del NLHPC (soporte@nlhpc.cl) mediante un correo.

```
at@ soporte@nlhpc.cl
Asunto: Instalacion tool Meme Suite:
_______________________________________

Correo.....

```
En nuestro correo de solicitud debemos agregar:

> El link de la tool a instalar. <br>
> El o los usuarios a los que se desea instalar la tool.

En el caso de que nuestra tool sea requerida por todo nuestro Team, existe la posibilidad de implementar la herramienta como Modulo, y que quede en el registro de tools instaladas del NLHPC para que pueda ser cargada por cualquier usuario, inclusive fuera de nuestro Team.

### Module Load 

El NLHPC tiene pre-instaladas una variedad de tools las cuales han sido testeadas y deberian ejecutarse sin problemas en cualquier cuenta del servidor.

Para acceder al catalogo de herramientas pre-instaladas, podemos presionar en la consola:

```
$ module load [TAB]
Display all 1113 possibilities? (y or n)
amber                                         MCTDH
Amber                                         MCTDH/86.3
amber/20-mpi-zen4-w                           mercurial
Amber/22-fosscuda                             mercurial/6.7.3-zen4-g
Amber/22.intel-2019b                          merra2wps
Amber/24-foss-2023b                           merra2wps/08-2021
amber/24-rocm-gcc-14.2.0-zen4                 MESH
amdblis                                       MESH/1.4
........
........
........

```

Este comando listara todas las tools existentes, en el caso de buscar una nombre especifico, podemos poner las inciales o el nombre completo.

```
$ module load M[TAB]
M4                                       MCR/R2018a                               Mono
M4/1.4.17                                MCR/R2020b                               Mono/6.12.0.122
M4/1.4.18                                MCTDH                                    Mothur/intel2022.00
M4/1.4.19                                MCTDH/86.3                               Mothur/intel2022.00/1.48.1
Magics                                   MEGAHIT                                  MPC
Magics/4.13.0                            MEGAHIT/1.2.9                            MPC/1.0.1
Mako                                     Mesa                                     MPC/1.2.1
Mako/1.1.4                               Mesa/21.1.7                              MPFR
MALT                                     MESH                                     MPFR/2.4.2
MALT/0.5.2                               MESH/1.4                                 MPFR/3.1.2
Mathematica                              MESH/1.4.2-symbols                       MPFR/4.1.0
Mathematica/13.3                         Meson                                    MPPCrystal17
MathGL                                   Meson/0.58.2                             MPPCrystal17/1.0.2
MathGL/8.0.1                             MetaBAT                                  MuJoCo
MathWorksServiceHost                     MetaBAT/2.15                             MuJoCo/2.1.1
MathWorksServiceHost/2024.13.0.2         METIS                                    MultiNest
Matlab                                   METIS/5.1.0                              MultiNest/3.10
MATLAB                                   Miniconda2                               MultiQC
Matlab/2017                              Miniconda2/4.7.10                        MultiQC/1.14
MATLAB/2019b                             Miniconda3                               MUMmer
Matlab-Runtime                           Miniconda3/4.5.12                        MUMmer/4.0.0beta2
Matlab-Runtime/amd                       Miniconda3/4.9.2                         MUMmer/4.0.0rc1
Matlab-Runtime/intel                     MinPath                                  MUMPS
Maven                                    MinPath/1.6                              MUMPS/5.4.0-metis
Maven/3.6.3                              Molekel                                  MUMPS/5.5.1-metis
MCR                                      Molekel/5.4.0-Linux_x86_64               MUMPS/5.7.3-metis
MCR/R2016b                               Molpro
MCR/R2017a                               Molpro/mpp-2020.2.1.linux_x86_64_openmp
```

El comando module load o ml para abreviar, es sencible a mayusculas y minisculas, por lo que:
```
$ module load M[TAB]
$ module load m[TAB]
$ module load ME[TAB]
$ module load Me[TAB]
$ module load me[TAB]
```
Entregara diferentes resultados.

Ademas, existen diferentes versiones para las tools pre-instaladas, por lo que habra que poner atención a la hora de cargar la tool y version correctas.

```
$ module load Java
Java                        Java/17.0.2                 Java/1.8.0_202
Java/11                     Java/17.0.4                 Java/1.8.0_232-b09-OpenJDK
Java/11.0.2                 Java/1.8                    Java/23.0.2
```








