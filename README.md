# cloudsovereignty-showcase-supplierdomain
supplierdomain is a part of a showcase implementation which is running on a open liberty instance. It is structured right now like this

- **supplierdomainParent** Parent maven module
    - **supplierdomainDTO** - contains all classes used in the rest controllers
    - **supplierdomainWAR** - contains the rest controllers and all EJB classes and entities
    - **supplierdomainEAR** - contains the war module

and could be found under the src folder

## The project consists of the following packages

- **de.novatec.showcase.supplier.dto** - with all related order domain dto's
- **de.novatec.showcase.supplier.ejb.entity** - with all related order domain entities
- **de.novatec.showcase.supplier.ejb.session** - with the order domain EJB session beans
- **de.novatec.showcase.supplier.controller** - with corresponding REST controllers for Item, Customer and Order
- **de.novatec.showcase.supplier.mapper** - with orika mapper fro dto/entity mapping

## Environment Variables

| Environment Variable         | Description                                             |
|------------------------------|---------------------------------------------------------|
| HTTP_PORT                    | Port on which the application listens for HTTP requests |
| HTTPS_PORT                   | Port on which the application listens for HTTPS requests |
| DB_HOST                      | Hostname or IP address of the database server           |
| DB_PORT                      | Port number for connecting to the database              |
| DB_SCHEMA                    | Database schema to use                                   |
| DB_NAME                      | Name of the database                                     |
| DB_USER                      | Username for database authentication                    |
| DB_PASSWORD                  | Password for database authentication                    |
| MANUFACTURE_DELIVER_URL      | URL endpoint for delivering components to the manufacture service |
| MANUFACTURE_USER             | Username for authenticating with the manufacture service |
| MANUFACTURE_PASSWORD         | Password for authenticating with the manufacture service |


## build, run and stop supplierdomain on an open liberty server
- **build:** mvn clean install
- **run:** mvn liberty:run
- **stop:** mvn liberty:stop
- **run open liberty in development mode:** mvn liberty:dev

All commands have to be executed from the supplierdomainEAR folder. In development mode you can run the the integration tests (*IT.java classes) by pressing RETURN/ENTER when the server is up. Code changes in the IT tests are hot replaced.

## Smoketest
There is a little script smoketest.sh in the supplierdomainParent\resources\smoketest folder which could be used to test if the very basic functionality works after staring the open liberty server with the supplierdomain as EAR. Be careful this smoketest.sh could be run only once!!!

- create three Suppliers
- create five SupplierComponents
- do a purchase with an existing Supplier
- do a purchase with a non existing Supplier
- do a delivery for the PurchaseOrder with id 1 from the first purchase call

The smoketest.sh script consist of two sub scripts - the setup-db.sh and business-calls.sh script. The first one setup the database of the orderdomain via some REST calls. The data for the calls could be found in the folder ./resources/smoketest/data. The smoketest script additionally starts/stops a mockserver which is used for emulating the manufature domain in the business calls. The exceptations for the calls could also be found in data folder. All three scripts have the optional parameters -h for setting the host and -p for setting the port of the domain which is called. The host defaults to localhost and port to 9080.

## openAPI
check [openAPI](http://localhost:9080/api/explorer/) if the server is running for the  API of the domain
