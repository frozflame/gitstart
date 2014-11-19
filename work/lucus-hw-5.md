
Answers to ASSIGNMENT # 5
-------------------------

All codes test on Ubuntu Linux, with Python 2.7.6 and 3.4.0. Compatibility to
other versions and systems are unknown.

Note: In folder `all`, files `run{0,1,2,3}` are slightly modified to be runable
under Linux system. 

=======================================

#### Code for Problem 1: `wrapDL.c` ####

```c
#include <stdlib.h>
#include <stdio.h>
#include <dlfcn.h>

void temperature(int n, double xyz[n][3], double u[n]){

    void (*func)(int, double[n][3], double u[n]); // t1
    void *handle = dlopen("./heat.dll", RTLD_LAZY);
    char *error;

    if (!handle){
        fprintf(stderr, "%s\n", dlerror());
        exit(1);
    }

    func = dlsym(handle, "temperature");

    if ((error = dlerror()) != NULL){
        fprintf(stderr, "%s\n", dlerror());
        exit(1);
    }

    func(n, xyz, u);
}
```

=======================================

#### Code for Problem 2a: `main.py`

```python
from __future__ import print_function
import sys
import time
import numpy as np
import itertools as it
import pylab as pl


if sys.version.startswith('3'):
    xrange = range

def main(temperature):
    # number of grid lilnes from face to middle
    N = 21
    
    # number of grid points in octant
    n = N * (N+1) / 2

    X = np.linspace(0, .5, N)
    Y = np.linspace(0, .5, N)

    # list of grid points
    xyz = np.empty([n, 3], np.double)

    k = 0
    for i in xrange(N):
        for j in xrange(i+1):
            xyz[k,0] = X[i];
            xyz[k,1] = Y[j]
            k += 1

    xyz[:,2] = .5

    # calculate temperatures, u
    t = time.clock()
    u = temperature(xyz)
    t = time.clock() - t 
   
    print("time = {}".format(t))

    # 2D array of temperatures
    U = np.empty([N, N])

    k = 0
    for i in xrange(N):
        for j in xrange(i+1):
            U[i,j] = u[k]
            U[j,i] = u[k]
            k += 1
    
    # print a table
    # step = (N-1) / 5
    # for j in xrange(N-1, -1, -step):
    #     for i in xrange(0, N, step):
    #         print("{:5.2f}".format(U[i,j]), end=' ')
    #     print()

    # contour plot
    xmesh, ymesh = np.meshgrid(X, Y)
    pl.contourf(xmesh, ymesh, U)
    pl.savefig("temperature.png")

    Uav = 0.
    for i in xrange(1, N):
        for j in xrange(1, N):
            Uav += U[i-1,j-1] + U[i-1,j] + U[i,j-1] + U[i,j]
    
    Uav /= (4. * (N-1) * (N-1))
    print("Uav =", Uav)
            
if __name__ == "__main__":
    if len(sys.argv) > 1 and sys.argv[1].lower() == 'disk':
        from wrapDisk import temperature
    else:
        from wrapDL import temperature
    main(temperature)
```

=======================================

#### Code for Problem 2b: `wrapDL.py` #### 

```python
import numpy as np
import ctypes as ct

ctemperature = ct.CDLL('./heat.so').temperature

def temperature(xyz):
    n = len(xyz)
    u = np.empty(n, np.double)
    
    if xyz.dtype != np.double:
        xyz = xyz.astype(np.double);

    ctemperature(
       ct.c_int(n),
       xyz.ctypes.data_as(ct.c_voidp),
       u.ctypes.data_as(ct.c_voidp)
    ) 

    return u
```

=======================================

#### Code for Problem 3a: `heatpgm.c` ####

```c
#include <math.h>
#include <time.h>
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <stdint.h>

static double outcome(double xyz[3]);

void main(){

    int Nt = 5000;  // number of trials

    /* suffix with i to distinguish */
    double (*xyz)[3];
    double *u;
    int32_t n;

    fread(&n, sizeof(int32_t), 1, stdin);

    xyz = (double (*)[3]) malloc(3 * sizeof(double) * n);
    u = (double *) malloc(sizeof(double)*n);


    for (int i =0; i < n; i++){
        fread(xyz + i, sizeof(double), 3, stdin);
    }


    srand(time(NULL));
    for (int i = 0; i < n; i++){
        u[i] = 0.;
        for (int k = 0; k < Nt; k++)
            u[i] += outcome(xyz[i]);
        u[i] /= (double)Nt;
    }

    for (int i =0; i < n; i++){
        fwrite(u + i, sizeof(double), 1, stdout);
    }

    return;
}

static double outcome(double xyz[3]){
    double dmin = 0.001;  // nearness to boundary before stopping
    double x = xyz[0], y = xyz[1], z = xyz[2];
    double u;
    while (true){
        // calculate distance to boundary
        double dx = x > 0.5 ? 1. - x : x;
        double dy = y > 0.5 ? 1. - y : y;
        double dz = z > 0.5 ? 1. - z : z;
        double d = dy < dx ? dy : dx;
        u = 0.;
        if (dz < d){d = dz; u = 100.;}
        if (d < dmin) break;
        double rx, ry, rz, r;  // generate a random direction
        do {
            rx = 2.*(double)rand()/(double)RAND_MAX - 1.;
            ry = 2.*(double)rand()/(double)RAND_MAX - 1.;
            rz = 2.*(double)rand()/(double)RAND_MAX - 1.;
            r = pow(rx*rx + ry*ry + rz*rz, 0.5);}
        while (r > 1.);
        x += d*rx/r; y += d*ry/r; z += d*rz/r;}
    return u;
}

```

=======================================

#### Code for Problem 3b: `wrapPipe.py` ####

```python

from subprocess import Popen, PIPE
import numpy as np


def temperature(xyz):
    n = len(xyz)
    
    proc = Popen('./heatpgm.exe', shell=True, stdin=PIPE, stdout=PIPE,\
        stderr=PIPE)

    idata = np.array([n], np.int32).tostring()
    idata += xyz.tostring()

    odata, edata = proc.communicate(input=idata)

    u = np.frombuffer(odata, np.double, n)
    return u
```
