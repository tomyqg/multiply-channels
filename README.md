multiply-channels
===

This project provides a commandline tool to create knxprod files for ETS.

It is motivated by this [knx](https://github.com/thelsing/knx) stack and the according [CreateKnxProd](https://github.com/thelsing/CreateKnxProd) tool.

The current version provides the following verbs:

- **create**     Check given xml file and create knxprod

- **check**      Execute sanity checks on given xml file

- **knxprod**    Create knxprod file from given xml file without checks

- **new**        Create new xml file with a fully commented and working mini exaple

- **help**       Display more information on a specific command.

- **version**    Display version information.

This tool also creates a header file with defines for all parameter and com object definitions in the xml. An ETS must be installed on the PC. Currently ETS 4, ETS 5.5, ETS 5.6 and ETS 5.7 are supported. The correct ETS converter version is automatically found dependent on xmlns of provided xml document.
This project uses dotnet core 3.0.

### Examples:

- multiplychannels new --ProductName=TempSensor --AppNumber=567 Sensor

    Creates initial Sensor.xml, do sanity checks produce Sensor.h, produce Sensor.knxprod

- multiplychannels create Sensor

    Reads Sensor.xml, do sanity checks, produce Sensor.h, produce Sensor.knxprod

- multiplychannels knxprod -o device.knxpord Sensor.xml

    Reads Sensor.xml, produce device.knxprod

- multiplychannels check Sensor.xml

    Reads Sensor.xml, do sanity checks

### Tipps:

If all sanity checks were OK and the knxprod file was created, there might be still problems using this file in ETS. Because the user is editing an xml file, there might be many other problems there, which are not checked by this tool yet.

As a general hint:

- if there is a problem importing the knxprod file into the product catalog (import function in ETS), there is usually a problem with Parameters-, ParameterTypes-, ComObjects-Section or the document structure itself. I.e. a dash in SerialNumber prevented an import, even though the creation of knxprod worked fine (in the meantime there is a check for SerialNumber).

- if import was successful, but you cannot add the device to your project, usually there is a problem in Dynamic-, ParameterRef-, ComObjectRef-Section.

If you find a situation, which is not yet checked but leads to errors in ETS, tell me and I will add a new check. Or create a pull request...
