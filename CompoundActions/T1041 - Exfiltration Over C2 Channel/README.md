# T1041 - Exfiltration via C2 Channel

This compound action uploads sample DLP test data provided by dlptest.com It then exfiltrates the data through the C2 channel used by the SCYTHE payload to communicate with the SCYTHE server.

It is recommended you try this as HTTP and HTTPS, especially TLS decryption is not enabled outbound.

Save the files in the VFS folder in VFS:/shared/DLPTest 