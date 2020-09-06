# Excel Tips useful for Cloud Platform

- [Excel Tips useful for Cloud Platform](#excel-tips-useful-for-cloud-platform)
  - [Generate UUID in excel for CAPM](#generate-uuid-in-excel-for-capm)




## Generate UUID in excel for CAPM
Use the following formula to generate a UUID for CAPM
```sh
=CONCATENATE(DEC2HEX(RANDBETWEEN(0,4294967295),8),"-",DEC2HEX(RANDBETWEEN(0,42949),4),"-",DEC2HEX(RANDBETWEEN(0,42949),4),"-",DEC2HEX(RANDBETWEEN(0,42949),4),"-",DEC2HEX(RANDBETWEEN(0,4294967295),8),DEC2HEX(RANDBETWEEN(0,42949),4))
```