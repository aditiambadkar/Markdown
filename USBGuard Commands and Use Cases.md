# USBGuard Commands and Use Cases

1. list-rules: List the rule set (policy) used by the USBGuard daemon.

```
$ sudo usbguard list-rules
1: allow id 1d6b:0002 serial "0000:00:0b.0" name "EHCI Host Controller" hash "SEiVqUWwefEKDMN9OJUyXkFIvvFPJmvPTRKIlVCvlvE=" parent-hash "XD9lEJg5Feonf6Uko19yKqHyZdCPMmirFBPgSumjIh0=" with-interface 09:00:00
2: allow id 1d6b:0001 serial "0000:00:06.0" name "OHCI PCI host controller" hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" parent-hash "q5qcdVMftU5RxwqKfaqqy/8ovn93tSvpOOQt8fzkfZQ=" with-interface 09:00:00
3: allow id 80ee:0021 serial "" name "USB Tablet" hash "8S88DbsXkyb93aEG099kxcbjrHSGfpZEJ8W0048wl1A=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" via-port "2-1" with-interface 03:00:00
4: allow id 17ef:608d serial "" name "Lenovo USB Optical Mouse" hash "klpDZuv1jhWGNqZLOl+KXF+75Ir3PfBm6D6ncjoLRBU=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" with-interface 03:01:02
5: allow id 04d9:1702 serial "" name "USB Keyboard" hash "Ds5ZasGHmjjrerHggesWZ7FwItiqZjztdEZGp/w3VnQ=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" with-interface { 03:01:01 03:00:00 }
```

2. list-devices: List all USB devices recognized by the USBGuard daemon.

```
$ sudo usbguard list-devices
6: allow id 1d6b:0002 serial "0000:00:0b.0" name "EHCI Host Controller" hash "SEiVqUWwefEKDMN9OJUyXkFIvvFPJmvPTRKIlVCvlvE=" parent-hash "XD9lEJg5Feonf6Uko19yKqHyZdCPMmirFBPgSumjIh0=" via-port "usb1" with-interface 09:00:00
7: allow id 1d6b:0001 serial "0000:00:06.0" name "OHCI PCI host controller" hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" parent-hash "q5qcdVMftU5RxwqKfaqqy/8ovn93tSvpOOQt8fzkfZQ=" via-port "usb2" with-interface 09:00:00
8: allow id 80ee:0021 serial "" name "USB Tablet" hash "8S88DbsXkyb93aEG099kxcbjrHSGfpZEJ8W0048wl1A=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" via-port "2-1" with-interface 03:00:00
```

3. allow-device [OPTIONS] id: Authorize a device identified by the device id to interact with the system.

```
$ sudo usbguard allow-device [-p] <id>

-p: Make the decision permanent. A device specific allow rule will be appended to the current policy.
```

4. block-device [OPTIONS] id: Deauthorize a device identified by the device id.

```
$ sudo usbguard block-device [-p] <id>

-p: Make the decision permanent. A device specific block rule will be appended to the current policy.
```

5. remove-rule id: Remove a rule identified by the rule id from the rule set.

```
$ sudo usbguard remove-rule <id>
```

6. append-rule rule: Append the rule to the current rule set.

```
$ sudo usbguard append-rule 'allow id 04d9:1702 serial "" name "USB Keyboard" hash "Ds5ZasGHmjjrerHggesWZ7FwItiqZjztdEZGp/w3VnQ=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" with-interface { 03:01:01 03:00:00 }'
```

7. watch: Watch the IPC interface events and print them to stdout.

```
$ sudo usbguard watch
[IPC] Connected
[device] PresenceChanged: id=10
 event=Remove
 target=block
 device_rule=block id 17ef:608d serial "" name "Lenovo USB Optical Mouse" hash "klpDZuv1jhWGNqZLOl+KXF+75Ir3PfBm6D6ncjoLRBU=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" via-port "2-3" with-interface 03:01:02
[device] PresenceChanged: id=13
 event=Insert
 target=block
 device_rule=block id 17ef:608d serial "" name "Lenovo USB Optical Mouse" hash "klpDZuv1jhWGNqZLOl+KXF+75Ir3PfBm6D6ncjoLRBU=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" via-port "2-3" with-interface 03:01:02
[device] PolicyChanged: id=13
 target_old=block
 target_new=block
 device_rule=block id 17ef:608d serial "" name "Lenovo USB Optical Mouse" hash "klpDZuv1jhWGNqZLOl+KXF+75Ir3PfBm6D6ncjoLRBU=" parent-hash "lUN32sIeMBBlD8Pd82mxu95iCTw8oKlT8iZDeg628/o=" via-port "2-3" with-interface 03:01:02
 rule_id=4294967294
```
