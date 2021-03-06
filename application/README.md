# Customized Metrics Application

This application will generate metrics related to VXLAN fabrics, specifically
traffic generation related to the underlay routed interface and Type-2 or
L2 routes.

The **vxlan.py** file relates to metrics found in the VXLAN Grafana
dashboard. The **routing.py** file relates to metrics found in the IP Prefix
Grafana dashboard.

The metrics are generated by NX-OS 'show' commands that are delivered and
processed using the NX-API capability of NX-OS. These commands are found
in each of the metric's related methods.

## Application Requirements

Prior to running this application on the command line (outside of the
containerized version), you will need to create a Python virtual environment
to install the required Python dependencies. The process begins with installing
the [NXAPI](../nxapi/README.md) library.

After installing the base NXAPI package, you'll need to install the additional
Python package requirements for this application - while the virtual environment
is activated - via:

```bash
pip3 install -r requirements.txt
```

## Application Execution

```bash
usage: generate.py [-h] [-c] [-t TARGET] [-p PORT] [-u USER] [-w PASSWORD] [-v] [-s] [-x]

optional arguments:
  -h, --help            show this help message and exit
  -t TARGET, --target TARGET
                        Provide remote hostname/IP for NXAPI
  -p PORT, --port PORT  Provide remote port for NXAPI
  -u USER, --user USER  Provide remote username for NXAPI
  -w PASSWORD, --password PASSWORD
                        Provide remote password for NXAPI
  -s, --ssl             Connect via SSL for NXAPI
  -v, --verbose         Enable verbose output
  -c, --container       Flag container operation

```

### Verbose/Debugging invocation

If you invoke the script from the command line with the verbose option,
you will see the results of the metric generation at the command line.

### Normal, non-containerizd invocation

Without the verbose flag, the script silently loops in the foreground
and the metrics generated can be viewed on the localhost port of 8888.
This is the same port and data consumed by Prometheus.

### Containerized invocation

Invoking the script with the container flag will result in the script
overriding any CLI flags and looking for the target, port, user, and
password values in the environment variables:

- NXAPI_HOST: Switch hostname/IP, defaults to 'host.docker.internal'
- NXAPI_PORT: Switch NXAPI port, defaults to 23456
- NXAPI_USER: Switch username, defaults to 'admin'
- NXAPI_PASS: Switch password, defaults to 'admin'
