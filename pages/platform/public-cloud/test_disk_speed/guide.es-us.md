---
title: Comprobar la velocidad de los discos
excerpt: Comprobar la velocidad de los discos
slug: comprobar_la_velocidad_de_los_discos
legacy_guide_number: g1956
section: Almacenamiento
updated: 2022-01-04
---

> [!primary]
> Esta traducción ha sido generada de forma automática por nuestro partner SYSTRAN. En algunos casos puede contener términos imprecisos, como en las etiquetas de los botones o los detalles técnicos. En caso de duda, le recomendamos que consulte la versión inglesa o francesa de la guía. Si quiere ayudarnos a mejorar esta traducción, por favor, utilice el botón «Contribuir» de esta página.
>

**Última actualización: 12/05/2023**

## Objetivo

Es probable que desee comprobar la velocidad de sus discos, ya sea para comparar el rendimiento de las distintas unidades o para comprobar si las prestaciones son las correctas. 

**Esta guía explica cómo verificar el número de entradas/salidas por segundo (IOPS) que sus discos son capaces de realizar, tanto para los discos de instancias como para los discos adicionales.**


## Requisitos

- Tener una [instancia Public Cloud](https://www.ovhcloud.com/es/public-cloud/) en su cuenta de OVHcloud.
- Tener acceso administrativo (root) a esta instancia por SSH (solo para Linux).


## Procedimiento

### Instalar el comando para hacer pruebas

El comando que necesita para comprobar la velocidad del disco se denomina `fio`. No está presente por defecto en el servidor.

Para instalar el `fio`, conéctese a su instancia por SSH y ejecute el siguiente comando:

```
root@server:~$ apt-get install fio
```

### Probar la velocidad del disco:

Si desea comprobar la velocidad de sus discos, ejecute el siguiente comando: 


```
root@server:~$ fio --name=rand-write --ioengine=libaio --iodepth=32 --rw=randwrite --invalidate=1 --bsrange=4k:4k,4k:4k --size=512m --runtime=120 --time_based --do_verify=1 --direct=1 --group_reporting --numjobs=1
```

> [!primary] 
>
> Deberá adaptar el argumento `--numjobs` al número de CPU de su instancia. 
> 
> Puede consultar la lista de argumentos y sus funciones directamente en el [manual de fio](https://github.com/axboe/fio/blob/master/HOWTO).
> 

Para comprobar el rendimiento de un disco adicional, deberá acceder a una de las carpetas del punto de montaje. 


```
root@server:~$ cd /mnt/disk
```

### Analizar los datos

Tras ejecutar este comando, obtendrá un resultado similar al siguiente: 


```
fio-2.1.11
Starting 1 process
test: Laying out IO file(s) (1 file(s) / 1024MB)
Jobs: 1 (f=1): [w(1)] [40.9% done] [0KB/3580KB/0KB /s] [0/895/0 iops] [eta 02m:55s] 
test: (groupid=0, jobs=1): err= 0: pid=12376: Thu Oct 29 14:46:37 2015
write: io=428032KB, bw=3566.2KB/s, iops=891, runt=120031msec
slat (usec): min=4, max=4640, avg=22.57, stdev=62.14
clat (usec): min=299, max=181699, avg=34778.45, stdev=7857.92
lat (usec): min=324, max=181769, avg=34801.55, stdev=7843.84
clat percentiles (usec):
| 1.00th=[ 708], 5.00th=[30848], 10.00th=[33536], 20.00th=[34560],
| 30.00th=[35072], 40.00th=[35072], 50.00th=[35072], 60.00th=[35584],
| 70.00th=[36096], 80.00th=[36608], 90.00th=[37632], 95.00th=[39680],
| 99.00th=[47360], 99.50th=[51968], 99.90th=[125440], 99.95th=[146432],
| 99.99th=[181248]
bw (KB /s): min= 2646, max= 4232, per=100.00%, avg=3567.77, stdev=136.56
lat (usec) : 500=0.23%, 750=1.26%, 1000=1.22%
lat (msec) : 2=0.37%, 4=0.03%, 10=0.01%, 20=0.11%, 50=96.05%
lat (msec) : 100=0.58%, 250=0.14%
cpu : usr=0.34%, sys=1.80%, ctx=9281, majf=0, minf=8
IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=100.0%, >=64=0.0%
submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.1%, 64=0.0%, >=64=0.0%
issued : total=r=0/w=107008/d=0, short=r=0/w=0/d=0
latency : target=0, window=0, percentile=100.00%, depth=32

Run status group 0 (all jobs):
WRITE: io=428032KB, aggrb=3566KB/s, minb=3566KB/s, maxb=3566KB/s, mint=120031msec, maxt=120031msec

Disk stats (read/write):
vda: ios=0/300294, merge=0/1455, ticks=0/7431952, in_queue=7433124, util=99.05%
```

La información que nos interesa corresponde a las IOPS, que podemos encontrar en la línea 6 del resultado: 


```
write: io=428032KB, bw=3566.2KB/s, iops=891, runt=120031msec
```

En este ejemplo, podemos ver cómo las prestaciones del disco corresponden a 891 iops aproximadamente.


## Más información

[Crear y configurar un disco adicional en una instancia](https://docs.ovh.com/us/es/public-cloud/crear_y_configurar_un_disco_adicional_en_una_instancia/)

Interactúe con nuestra comunidad de usuarios en <https://community.ovh.com/en/>.
