MPI
Configuración de Servidores
MPI cluster
Tutorial MPI linux


Configurar teclado
sudo dpkg-reconfigure keyboard-configuration

IP estática
sudo pico /etc/network/interfaces

Para mi configuración:

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static

address 192.168.100.100 --- 192.168.100.101 ...
netmask 255.255.255.0
network 192.168.100.0
broadcast 192.168.100.255
gateway 10.0.2.15

Generar SSH Key
ssh-keygen -t dsa
    Enviar Master - Slave(Crea copia del archivo en el otro servidor)
scp id_dsa.pub slave@ip-slave:~/.ssh/id_dsa.pub
cat is_dsa.pub >> authorized_keys (Copiar en Archivo authorized_keys)


MPICH2
sudo apt-get install libcr-dev mpich2 mpich2-doc

Hola Mundo
/* C Example */
#include <mpi.h>
#include <stdio.h>
 
int main (int argc, char* argv[])
{
  int rank, size;
 
  MPI_Init (&argc, &argv);      /* starts MPI */
  MPI_Comm_rank (MPI_COMM_WORLD, &rank);        /* get current process id */
  MPI_Comm_size (MPI_COMM_WORLD, &size);        /* get number of processes */
  printf( "Hello world from process %d of %d\n", rank, size );
  MPI_Finalize();
  return 0;
}

To compile and execute your application run the following commands:

danon@danon-laptop:~$ mpicc mpi_hello.c -o hello
danon@danon-laptop:~$ mpirun -np 2 ./hello
Hello world from process 0 of 2
Hello world from process 1 of 2
danon@danon-laptop:~$

