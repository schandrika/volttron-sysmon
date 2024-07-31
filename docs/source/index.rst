volttron-sysmon
===============

The System Monitoring Agent (colloquially “SysMon”) can be installed on the platform to monitor system resource metrics, including but not limited to percent CPU utilization, percent system memory (RAM) utilization, and percent storage (disk) utilization based on disk path.

Requires
--------

* python >= 3.10
* volttron >= 10.0

Installation
------------

Before installing, VOLTTRON should be installed and running. Its virtual environment should be active. Information on how to install the VOLTTRON platform can be found `here <https://github.com/eclipse-volttron/volttron-core>`_.

Create a directory called ``config`` and use the change directory command to enter it.

.. code-block:: shell

    mkdir config
    cd config

After entering the config directory, create a file named ``sysmon_agent_config.json``, use the below JSON to populate your new file.

For simplicity, copy all of the JSON from below and switch the key ``"poll": false,`` to ``"poll": true,`` for each system resource you want to monitor.

.. code-block:: json

    {
        "default_publish_type": "datalogger",
        "base_topic": "Log/Platform",
        "monitor": {
            "cpu_percent": {
                "point_name": "CPU/Percent",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_cpu": true,
                    "capture_interval": null
                }
            },
            "cpu_times": {
                "point_name": "CPU/Times",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_cpu": false,
                    "sub_points": {
                        "user": false,
                        "nice": false,
                        "system": false,
                        "idle": false,
                        "iowait": false,
                        "irq": false,
                        "softirq": false,
                        "steal": false,
                        "guest": false,
                        "guest_nice": false
                    }
                }
            },
            "cpu_times_percent": {
                "point_name": "CPU/TimePercentages",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_cpu": false,
                    "capture_interval": null,
                    "sub_points": {
                        "user": false,
                        "nice": false,
                        "system": false,
                        "idle": false,
                        "iowait": false,
                        "irq": false,
                        "softirq": false,
                        "steal": false,
                        "guest": false,
                        "guest_nice": false
                    }
                }
            },
            "cpu_statistics": {
                "point_name": "CPU/Statistics",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "sub_points": {
                        "ctx_switches": false,
                        "interrupts": false,
                        "soft_interrupts": false
                    }
                }
            },
            "cpu_frequency": {
                "point_name": "CPU/Frequencies",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_cpu": false,
                    "sub_points": {
                        "current": false,
                        "min": false,
                        "max": false
                    }
                }
            },
            "memory": {
                "point_name": "Memory",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "sub_points": {
                        "total": false,
                        "available": true,
                        "percent": true,
                        "used": true,
                        "free": false,
                        "active": false,
                        "inactive": false,
                        "buffers": false,
                        "cached": false,
                        "shared": false,
                        "slab": false
                    }
                }
            },
            "disk_usage": {
                "point_name": "Disk/Usage",
                "check_interval": 3600,
                "poll": true,
                "params": {
                    "disk_path": ["/"],
                    "sub_points": {
                        "total": false,
                        "used": true,
                        "free": true,
                        "percent": true
                    }
                }
            },
            "load_average": {
                "point_name": "CPU/LoadAverage",
                "check_interval": 5,
                "poll": true,
                "params": {
                    "sub_points": {
                        "OneMinute": true,
                        "FiveMinute": true,
                        "FifteenMinute": true
                    }
                }
            },
            "swap": {
                "point_name": "Swap",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "sub_points": {
                        "total": false,
                        "used": true,
                        "free": true,
                        "percent": true,
                        "sin": false,
                        "sout": false
                    }
                }
            },
            "path_usage": {
                "point_name": "Disk/Path/Usage",
                "check_interval": 3600,
                "poll": false,
                "params": {
                    "path_name": "/var/log/journal"
                }
            },
            "path_usage_rate": {
                "point_name": "Disk/Path/Rate",
                "check_interval": 3600,
                "poll": false,
                "params": {
                    "path_name": "/var/log/journal"
                }
            },
            "disk_io": {
                "point_name": "Disk/IO",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_disk": false,
                    "included_disks": [],
                    "no_wrap": true,
                    "sub_points": {
                        "read_count": false,
                        "write_count": false,
                        "read_bytes": true,
                        "write_bytes": true,
                        "read_time": true,
                        "write_time": true,
                        "read_merged_count": false,
                        "write_merged_count": false,
                        "busy_time": true,
                        "read_throughput": true,
                        "write_throughput": true
                    }
                }
            },
            "network_io": {
                "point_name": "Network/IO",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_nic": true,
                    "included_nics": [],
                    "no_wrap": true,
                    "sub_points": {
                        "bytes_sent": true,
                        "bytes_recv": true,
                        "packets_sent": true,
                        "packets_recv": true,
                        "errin": true,
                        "errout": true,
                        "dropin": true,
                        "dropout": true,
                        "receive_throughput": true,
                        "send_throughput": true
                    }
                }
            },
            "network_connections": {
                "point_name": "Network/Connections",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "kind": "inet",
                    "sub_points": {
                        "fd": false,
                        "family": false,
                        "type": false,
                        "laddr": false,
                        "raddr": false,
                        "status": false,
                        "pid": false
                    }
                }
            },
            "network_interface_addresses": {
                "point_name": "Network/Interface/Addresses",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "included_interfaces": [],
                    "sub_points": {
                        "family": false,
                        "address": false,
                        "netmask": false,
                        "broadcast": false,
                        "ptp": false
                    }
                }
            },
            "network_interface_statistics": {
                "point_name": "Network/Interface/Addresses",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "included_interfaces": [],
                    "sub_points": {
                        "isup": false,
                        "duplex": false,
                        "speed": false,
                        "mtu": false
                    }
                }
            },
            "sensors_temperatures": {
                "point_name": "Sensors/Temperatures",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "fahrenheit": false,
                    "included_sensors": [],
                    "sub_points": {
                        "label": true,
                        "current": true,
                        "high": true,
                        "critical": true
                    }
                }
            },
            "sensors_fans": {
                "point_name": "Sensors/Fans",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "included_sensors": [],
                    "sub_points": {
                        "label": false,
                        "current": false
                    }
                }
            },
            "sensors_battery": {
                "point_name": "Sensors/Battery",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "sub_points": {
                        "percent": false,
                        "secsleft": false,
                        "power_plugged": false
                    }
                }
            },
            "boot_time": {
                "point_name": "BootTime",
                "check_interval": 5,
                "poll": false,
                "params": {}
            },
            "users": {
                "point_name": "Users",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "sub_points": {
                        "name": false,
                        "terminal": false,
                        "host": false,
                        "started": false,
                        "pid": false
                    }
                }
            }
        }
    }

Besides ``poll``, there are four other important options in sysmon's configuration.

- ``default_publish_type`` only needs to be specified once in the configuration, this is the default publish type.
- ``base_topic`` also only needs to be specified once. This is the base topic.
- ``point_name`` changes the point name for the specific system monitor. In combination with publish_type and base_topic, our data for cpu_percent would be published to volttron with a topic of: **datalogger/Log/Platform/CPU/Percent** using the below JSON as an example.
- ``check_interval`` adjusts the time in seconds to poll for new system data. This can be modified for each system resource.

The Sysmon agent serves as a wrapper for psutil. You can adjust resource specific options by adjusting false to true in the configuration file. For detailed insights into these options and their impact, you can read the `psutil documentation <https://psutil.readthedocs.io/en/latest/>`_.

You may also delete any unused fields if desired. For example, a configuration to monitor just cpu_percent could look like this.

.. code-block:: json

    {
        "default_publish_type": "datalogger",
        "base_topic": "Log/Platform",
        "monitor": {
            "cpu_percent": {
                "point_name": "CPU/Percent",
                "check_interval": 5,
                "poll": false,
                "params": {
                    "per_cpu": true,
                    "capture_interval": null
                }
            }
        }
    }

Install and start the sysmon agent

.. code-block:: bash

    vctl install volttron-sysmon --vip-identity agent.sysmon --start

Add ``sysmon_agent_config.json`` to the configuration store

.. code-block:: bash

    vctl config store agent.sysmon config sysmon_agent_config.json

Observe Data
------------

To see data being published to the bus, install a `Listener Agent <https://pypi.org/project/volttron-listener/>`_:

.. code-block:: bash

    vctl install volttron-listener --start

Periodic Publish
----------------

At the interval specified by the configuration option for each resource, the agent will automatically query the system for the resource utilization statistics and publish it to the message bus using the topic as previously described. The message content for each publish will contain only a single numeric value for that specific topic. Currently, “scrape_all” style publishes are not supported.

The following is an example of the LoadAverage publish captured by the Listener agent in the VOLTTRON log:

.. code-block:: none

    2024-01-02 12:03:50,435 (volttron-listener-0.2.0rc0 2404) listener.agent(104) INFO: Peer: pubsub, Sender: volttron-sysmon-0.1.0_1:, Bus: , Topic: datalogger/Log/Platform/CPU/LoadAverage, Headers: {'Date': '2024-01-02T20:03:50.426814+00:00', 'min_compatible_version': '3.0', 'max_compatible_version': ''}, Message:
    {'FifteenMinute': {'Readings': ['2024-01-02T20:03:50.426814+00:00',
                                    0.009765625],
                       'Units': 'load_average',
                       'data_type': 'float',
                       'tz': 'UTC'},
     'FiveMinute': {'Readings': ['2024-01-02T20:03:50.426814+00:00', 0.05517578125],
                    'Units': 'load_average',
                    'data_type': 'float',
                    'tz': 'UTC'},
     'OneMinute': {'Readings': ['2024-01-02T20:03:50.426814+00:00', 0.14404296875],
                   'Units': 'load_average',
                   'data_type': 'float',
                   'tz': 'UTC'}}

Disclaimer Notice
-----------------

This material was prepared as an account of work sponsored by an agency of the United States Government. Neither the United States Government nor the United States Department of Energy, nor Battelle, nor any of their employees, nor any jurisdiction or organization that has cooperated in the development of these materials, makes any warranty, express or implied, or assumes any legal liability or responsibility for the accuracy, completeness, or usefulness or any information, apparatus, product, software, or process disclosed, or represents that its use would not infringe privately owned rights.

Reference herein to any specific commercial product, process, or service by trade name, trademark, manufacturer, or otherwise does not necessarily constitute or imply its endorsement, recommendation, or favoring by the United States Government or any agency thereof, or Battelle Memorial Institute. The views and opinions of authors expressed herein do not necessarily state or reflect those of the United States Government or any agency thereof.
