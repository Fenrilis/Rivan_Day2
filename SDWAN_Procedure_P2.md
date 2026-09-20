<img width="471" height="108" alt="{B532F118-447E-4C13-8189-2798D3B154F9}" src="https://github.com/user-attachments/assets/7a77d897-a722-4abe-b708-35c9c4866442" /><img width="881" height="348" alt="{1CB9E72C-0BF5-4797-90BF-FAF9381C7BA5}" src="https://github.com/user-attachments/assets/49415ed7-e0ae-4357-a9ed-b6ddef3caf82" /><img width="886" height="518" alt="{BFE3E1EF-E010-4DD3-B4C0-8778BA062632}" src="https://github.com/user-attachments/assets/62854a7b-1a39-4842-86e6-471e95cb0080" />
| Device | Port |
| --- | ---: |
| PKI SERVER | `32913` |
| vManage | `32897` |
| vSmart | `32898` |
| vBond | `32899` |
| vEdge-MINDANAO | `32904` |
| CSW-MINDANAO | `32907` |



Go to EVE|Topology

	power on the PKI server, TURN off vedge & csw visayas, and power vedge & and CSW mindanao
	!NOTE!
	WAIT FOR 10 MINS PKI SERVER TO PROPERLY SETUP
	BEFORE PROCEEDING TO PART 2 SD-WAN CA, PART 1 MUST COMPLETE AND PROPERLY CONFIGURED
	
	
<img width="249" height="233" alt="{93CEB256-089A-4BC8-9FDF-E999919986FB}" src="https://github.com/user-attachments/assets/4eb65c80-6402-4518-ba35-6739da3be336" />

<img width="823" height="579" alt="{E86A8596-0C95-4F6C-9F55-503FCD1D5F5C}" src="https://github.com/user-attachments/assets/3282a983-3008-4bbf-bc80-bb498c1f61a9" />

access the pki server & Vedge mindanao through secure crt telnet:

Credentials:
IPv4: 208.8.8.187
| PKI SERVER | `32913` |
| vEdge-MINDANAO | `32904` |

<img width="892" height="209" alt="{267CEC5F-A623-4374-A310-EF00BA93957B}" src="https://github.com/user-attachments/assets/9eb41b90-9e41-477e-ac7d-aa90aaadc78e" />

<img width="878" height="236" alt="{D9260403-AD85-439B-AD56-4F514F9CEF71}" src="https://github.com/user-attachments/assets/8f926cab-96f6-4031-854e-a27a600fcd79" />


Go to Vmanage GUI:

burger icon --> Configuration --> Certificates - send to controller

Expected Output:

<img width="902" height="418" alt="{4ABF98A6-8231-4461-83CB-4838976E87B0}" src="https://github.com/user-attachments/assets/abddc51e-d0d9-49d7-bddd-0f0118c48854" />

  
!@Go to PKI server:
	conf t
	crypto pki export rivanpki pem terminal
	!copy CA root

% CA certificate:
-----BEGIN CERTIFICATE-----
MIIDIDCCAgigAwIBAgIBATANBgkqhkiG9w0BAQsFADAhMR8wHQYDVQQDExZyb290
Y2EuUklWQU5DT1JQLmxvY2FsMB4XDTI2MDExODE5MDIxMloXDTI5MDExNzE5MDIx
MlowITEfMB0GA1UEAxMWcm9vdGNhLlJJVkFOQ09SUC5sb2NhbDCCASIwDQYJKoZI
hvcNAQEBBQADggEPADCCAQoCggEBANHmliLVoDJpoP/QYY9BYNoM5nYmqHTiWrcz
/edesixyK6l4a5e4sFVjFnUxf/+1ND4FIUE3zsDDJEtvmiziO+/ObM+e34uSvQKU
UoLIsUC96LQ+uwSrcWlA+0EYb9x+uHj1+sKKFE1n2paWcWHYxyy4Fdg0h/8vV4jJ
/yLvPrsI0Tp8HvZBMiNQmZihliNc9eiBToeWci3FkIbpoylOsih+Pt9gAjHisJpJ
2mATA0xcz5dt0DHM49zyIYUm4/F8i/NehDi98RanANgBlFVHHdIrcikAtqKq2usg
iTtxqfRDGfinEp7N2lQcflQmwkwrGrfpTC4FX5+QLtVRst//560CAwEAAaNjMGEw
DwYDVR0TAQH/BAUwAwEB/zAOBgNVHQ8BAf8EBAMCAYYwHwYDVR0jBBgwFoAUWTJM
3TFjBLb5mucfAOAjH+36gPQwHQYDVR0OBBYEFFkyTN0xYwS2+ZrnHwDgIx/t+oD0
MA0GCSqGSIb3DQEBCwUAA4IBAQA3f/bSd3vrB6u5F6nKMufwPoxVkRAnrTba1Ss+
jvnjJIZ0MbXnZdHaJyZM6Lof58HRE66Kg8sYeyd+VRHthSjR+rBGfqovUqm0mTeS
4NdwngebSbP/zrZKNsu7o/dazfJOdnNBrSqrWKoDliwXdtfrwWbei6/swX4WBVEF
EthIAgr2uvKKbKJleBk9j5spAz9JS9nAI2nJ0D/scFbpxcxHtjuNSypGxbvUA6E8
CihCAdhQxaGsO00S598LTCgtQepq3A0o39ER1u7L2Qa19lZXKr7jVVs7MTJlnXZo
dVb5NArbTAGGmpvcr8FdxjMN8LPBvD9a22GpnHUkZJxI1iah
-----END CERTIFICATE-----

<img width="755" height="655" alt="{BA2B9B71-3E0E-466E-A484-AC0CAF51CD65}" src="https://github.com/user-attachments/assets/f6b0d387-0cc8-42e1-88b0-3d5e2f3e89dc" />

NOTE:
copy the first - up to the last -


!@vedge-Mindanao Cisco:
vshell
cd /home/admin/
ls !for checking
cd pkicerts/
vi rivan.ca

<img width="884" height="206" alt="{6763D8E4-AD06-4A21-88AF-485C6DDE0F20}" src="https://github.com/user-attachments/assets/22d60d87-7528-4fef-a1ce-20709bb95852" />

!Warning
	!double enter!
	!press i!
	!copy ca root pki server and paste!

<img width="883" height="353" alt="{1D0F9941-9CE6-4529-9373-0CEBDD793039}" src="https://github.com/user-attachments/assets/397f3285-db60-4b57-a8d1-3b482739158a" />

	!press esc!
	:wq

<img width="886" height="348" alt="{31021CA1-5436-4EF8-AB27-CFF2A32AE1DA}" src="https://github.com/user-attachments/assets/de6a8c48-892f-4853-b090-29c4932937b0" />

	ls
  
expected output:

<img width="476" height="84" alt="{3554B0DF-49FC-416E-889E-F75AFFABAB60}" src="https://github.com/user-attachments/assets/183d57bd-049c-4917-92dd-6cd9ba44b8c6" />

exit

request root-cert-chain install /home/admin/pkicerts/rivan.ca 

Expected Output:

<img width="890" height="356" alt="{56C4DC37-C94D-4758-8330-D41664394A28}" src="https://github.com/user-attachments/assets/656a35bd-3322-4b5a-a3a7-f0dbf09b6b86" />



generate a CSR:
request csr upload /home/admin/pkicerts/min.csr

Enter organization-unit name : RIVANCORP
Re-enter organization-unit name : RIVANCORP

<img width="890" height="468" alt="{4E58B55C-5B45-4C94-954E-36FE45493840}" src="https://github.com/user-attachments/assets/455d38ad-a996-4913-a9b3-545b9bd86357" />

vshell
cat /home/admin/pkicerts/min.csr 

!copy CA request

-----BEGIN CERTIFICATE REQUEST-----
MIIDSTCCAjECAQAwgcgxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlh
MREwDwYDVQQHEwhTYW4gSm9zZTESMBAGA1UECxMJUklWQU5DT1JQMRYwFAYDVQQK
Ew1DaXNjbyBTeXN0ZW1zMUEwPwYDVQQDEzh2ZWRnZS01ZjRiZTE3Yi04ZTZhLTQ2
YWUtOTQ2Ny0zNWIyNmY1ZDU2OWEtMS52aXB0ZWxhLmNvbTEiMCAGCSqGSIb3DQEJ
ARYTc3VwcG9ydEB2aXB0ZWxhLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKDZHbxLY/sNb33mh0NkY1Empr2om9foe3QHOr8RCO2ID+ansVjgcSG+
oCdNJDf0tFdL1ErfR5sKAbDe6PXkMdW8JP1V7wiIKZL/61hA65PkWDsu7Q9dqYF+
P9EP1biclCgAiI0h4sZzGmRUHNlHnpVdXcCNOS27Bbma7TauPP9hSofWHgvS/FXz
MPI598m5xdxfkocabypD0oMAMi/4fPZW376oo69a5K8RriLTO5MmonAM3kaXqXBe
qk8NJJa7fTRmEg+LPWM3TlvCjUVBDISvEmtir8ii85y0rGdeVdgu9aOqoTHW3Vh9
BuuAMnPXPP41QFuZM+JFMepUVShw3esCAwEAAaA7MDkGCSqGSIb3DQEJDjEsMCow
CQYDVR0TBAIwADAdBgNVHQ4EFgQUeQ5dIVNA4/yP5NmdoCB5KKPDdbowDQYJKoZI
hvcNAQELBQADggEBACDXNqERcp0Z2d2d0rw+CEujlZ02cNCb2ZO7Ftg2OwAig29I
Sk6Mi1GmhR2Yc2+oyYPv/1XP8VjaatM0RUQNTZSMy9VxtwRKKhauYCzfPlxYZDjh
3OlZy5V6ht89KZ0eEDMsOSmdxB03gUpVnzuahCzeqM5eHqjE12g6QnAoL4SOAkBe
OLdXlc7Jlt4xROjulpu6MARHUh8V3pvuGVcNohEMWk7/2AsBfJxdmjUpoYEWGFHD
Y9oYpWL/B2omrFlYdwYFPRoL5fErBEbteduC9XTKhFwRdAHfg6pRw0kct0pFbs3G
6lsqAsj2fMgoFnRQLYx6sfIX7fX+oxU+duG86hQ=
-----END CERTIFICATE REQUEST-----

<img width="883" height="433" alt="{02A0202A-7AE7-4102-84F0-2AF284BE1646}" src="https://github.com/user-attachments/assets/e6a12257-d1cf-4b46-b190-7e7284e8d4bb" />



optional:
cd /home/admin/pkicerts/
openssl x509 -in rivan.ca -text -noout

!@pki-server:
crypto pki server rivanpki request pkcs10 terminal 

<img width="539" height="113" alt="{DAB3FD5E-2DCB-46DB-9A01-AB82A5F1E650}" src="https://github.com/user-attachments/assets/01006abc-83ef-490e-99d6-a24f4c83862a" />


!paste CERTIFICATE REQUEST!

<img width="527" height="341" alt="{A9506513-F669-4FD3-A54C-6D50777DF4B9}" src="https://github.com/user-attachments/assets/913f91a4-b106-4425-8bc1-06742f1cdefb" />

<img width="554" height="657" alt="{FBD59C17-15EB-46FC-9B82-DE867B9F5B9F}" src="https://github.com/user-attachments/assets/ab808b34-9338-43c4-a98a-77e37a01c593" />


!copy GRANTED CERTIFICATE!



% Granted certificate:
-----BEGIN CERTIFICATE-----
MIIDuDCCAqCgAwIBAgIBBzANBgkqhkiG9w0BAQsFADAhMR8wHQYDVQQDExZyb290
Y2EuUklWQU5DT1JQLmxvY2FsMB4XDTI2MDkyMDEyMDQzNloXDTI3MDkyMDEyMDQz
NlowgcgxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlhMREwDwYDVQQH
EwhTYW4gSm9zZTESMBAGA1UECxMJUklWQU5DT1JQMRYwFAYDVQQKEw1DaXNjbyBT
eXN0ZW1zMUEwPwYDVQQDEzh2ZWRnZS01ZjRiZTE3Yi04ZTZhLTQ2YWUtOTQ2Ny0z
NWIyNmY1ZDU2OWEtMi52aXB0ZWxhLmNvbTEiMCAGCSqGSIb3DQEJARYTc3VwcG9y
dEB2aXB0ZWxhLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKDZ
HbxLY/sNb33mh0NkY1Empr2om9foe3QHOr8RCO2ID+ansVjgcSG+oCdNJDf0tFdL
1ErfR5sKAbDe6PXkMdW8JP1V7wiIKZL/61hA65PkWDsu7Q9dqYF+P9EP1biclCgA
iI0h4sZzGmRUHNlHnpVdXcCNOS27Bbma7TauPP9hSofWHgvS/FXzMPI598m5xdxf
kocabypD0oMAMi/4fPZW376oo69a5K8RriLTO5MmonAM3kaXqXBeqk8NJJa7fTRm
Eg+LPWM3TlvCjUVBDISvEmtir8ii85y0rGdeVdgu9aOqoTHW3Vh9BuuAMnPXPP41
QFuZM+JFMepUVShw3esCAwEAAaNTMFEwDwYDVR0TAQH/BAUwAwEB/zAfBgNVHSME
GDAWgBRZMkzdMWMEtvma5x8A4CMf7fqA9DAdBgNVHQ4EFgQUeQ5dIVNA4/yP5Nmd
oCB5KKPDdbowDQYJKoZIhvcNAQELBQADggEBAC5iC/zOvyaU1go6SQJ5TxXf04QF
r2T/39mI5tfdgCW2IGMvJluohBNjuucTOWOVJsM2exkvjTfhJdsvD+lvFWGtE1aW
zvMp16WaF9JshSL7ApWPIydneTd9iyLn/EIvOA7M93fm4J2AEV22K+ZIYfQoDU2E
LbTVSqj84eshxhjuovVxqNgm5AMcDigMA4vW/NuYGGvnBKhgY3jGA2TOOmfww0Ge
iUsNrFeI2caWvx3b/SOGOOXfqZ1vMG8ezF6UaW9nziKx+tlrA5hcVmdPVKuAtDEb
M3hNM5GLoqUdaSlnkyHQs5LbvGh7hIhfD37gYKdEtn6dHtxiYrsHhTYbQnU=
-----END CERTIFICATE-----


vedge-mindanao cisco:
vshell
cd /home/admin/pkicerts/
vi grant.ca

<img width="411" height="105" alt="{E24078D5-716C-42D3-B0E2-E7CC5D98B6C2}" src="https://github.com/user-attachments/assets/c60cac27-79e6-4a47-b096-ee03ff934853" />

!double enter!
!press i!
!copy granted ca and paste!

<img width="881" height="348" alt="{1CB9E72C-0BF5-4797-90BF-FAF9381C7BA5}" src="https://github.com/user-attachments/assets/e80758ae-c6a6-48e1-81ff-098205f73aaf" />

!press esc!
:wq

<img width="876" height="353" alt="{C5434C6A-FBAD-46AA-B878-867DEA866599}" src="https://github.com/user-attachments/assets/4362d6dd-453f-47b3-8fb0-3601ed754198" />

ls

expected output:

<img width="471" height="108" alt="{B532F118-447E-4C13-8189-2798D3B154F9}" src="https://github.com/user-attachments/assets/0e40cad8-3930-4063-b243-b9bba712064c" />

exit

vedge-mindanao cisco:
request certificate install /home/admin/pkicerts/grant.ca

<img width="837" height="191" alt="{B7BCE8E6-3F77-4B28-9365-FE90F1066778}" src="https://github.com/user-attachments/assets/3136f0c2-404e-4dde-abba-45bc55df8c61" />

show certificate serial

!!!!
Chassis number: 5f4be17b-8e6a-46ae-9467-35b26f5d569a serial number: 07

vmanage & vbond:

request vedge add chassis-num 5f4be17b-8e6a-46ae-9467-35b26f5d569a serial-num 07

!optional!
vsmart:

request vedge delete chassis-num 5f4be17b-8e6a-46ae-9467-35b26f5d569a serial-num 07

burger icon --> configuration --> send to controller


!output!
CSW mindanao:

conf t
 hostname CSW-MINDANAO
 enable secret pass
 service password-encryption
 no logging console
 no ip domain lookup
 username admin priv 15 secret pass
 line vty 0 14
  transport input all
  password pass
  login local
  exec-timeout 0 0
 int lo0
  ip add 3.3.3.3 255.255.255.255
  exit
 int g0/0
  no sw
  ip add 172.16.9.2 255.255.255.252
  no shut
 int g0/1
  no sw
  ip add 10.1.3.2 255.255.255.252
  no shut
 router ospf 1
  router-id 3.3.3.3
  network 172.16.9.0 0.0.0.3 area 0
  network 3.3.3.3 0.0.0.0 area 0
  network 10.1.3.0 0.0.0.3 area 0
  passive-interface lo0
  end
  
  
burger icon --> configuration --> template --> device template
--> attach device --> attach vedge mindanao

ping 1.1.1.1
