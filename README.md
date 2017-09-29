# getnameinfo

`LD_PRELOAD` proof of concept.


Compile the shared object:

```
$ gcc -shared -ldl -fPIC getnameinfo.c -o getnameinfo.so
```

Run web100srv with `LD_PRELOAD`.

```
LD_LIBRARY_PATH=/home/iupui_ndt/build/lib \
  LD_PRELOAD=getnameinfo.so \
    /home/iupui_ndt/build/sbin/ndtd --tls_port 3010  \
      --private_key /etc/pki/tls/private/measurement-lab.org.key \
      --certificate /etc/pki/tls/certs/measurement-lab.org.crt \
      -dddddd --log_dir /var/spool/iupui_ndt  --snaplog --tcpdump --cputime  \
      --multiple --max_clients=40 --disable_extended_tests  \
      -f /home/iupui_ndt/build/ndt/web100_variables
```

Run a test, and all file names should use to the numeric client IP address.

