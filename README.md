# Quick SNMP (quicksnmp)
A simple way to use SNMP in your Python Scripts. Requires PySNMP.

This is not a python module, but just a script. With it, you can implement SNMP in your python scripts rapidly. Just copy this file into your project and use it as needed. *QuickSNMP is for quick scripts, don't use it in an application!*


```python
from pysnmp import hlapi
from . import quicksnmp

# Using SNMPv2c, we set the hostname of the remote device to 'SNMPHost'
quicksnmp.set('10.0.0.1', {'1.3.6.1.2.1.1.5.0': 'SNMPHost'}, hlapi.CommunityData('ICTSHORE'))

# Using SNMPv2c, we retrieve the hostname of the remote device
print(get('10.0.0.1', ['1.3.6.1.2.1.1.5.0'], hlapi.CommunityData('ICTSHORE')))

# We get interface name and Cisco interface description for all interfaces
# The last parameter is the OID containing the number of interfaces, so we can loop 'em all!
its = get_bulk_auto('10.0.0.1', [
    '1.3.6.1.2.1.2.2.1.2 ',
    '1.3.6.1.2.1.31.1.1.1.18'
    ], hlapi.CommunityData('ICTSHORE'), '1.3.6.1.2.1.2.1.0')
# We print the results in format OID=value
for it in its:
    for k, v in it.items():
        print("{0}={1}".format(k, v))
    # We leave a blank line between the output of each interface
    print('')
```
