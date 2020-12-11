# eIoT_API
API for integration with the eIoT Platform

## Authentication
In order to use the eIoT API you must obtain a set of credentials from the eIoT development team. Currently the only way to do that is to contact us at <eiotsubmission@gmail.com>. API authentication credentials must be provided as part of the query string of your API request.

Example: ```X.X.X.X:5000/api/scans?user=[USER]&pass=[PASS]```

## API Endpoints
There are two API endpoints available at this time:
```
/api/scans
/api/ddos
```

Each endpoint can return up to 10 records at a time to ensure the safety of our platform. The query syntax is the same for all of the API endpoints, although the fields and options available differ.

## Query Syntax
The query syntax is: ```[field]:[value] AND [field]:[value]```. Capitalization of field names is neccessary, and must be followed according to the field name definitions shown below. Additionally, the keyword ```AND``` must be capitalized. Capitalization of values can also impact the results retrieved from the database.

The queries should be returned as data in the request body, whereas authentication should be passed as a part of the query string. Any values that contain spaces should be wrapped in double quotation marks for accurate results. 

__Note:__ This syntax will be expanded in the future to support a more verbose set of keywords and operations.

## Field Options
#### /api/scans
- ip: IP address or IP range using slash notation
- startDate: “yyyy-mm-dd hh:mm:ss.s” format
- endDate: “yyyy-mm-dd hh:mm:ss.s” format
- label: “IoT” or “Desktop”
- country: String
- state: String
- city: String
- org: String (WHOIS Organization)
- sector: String (Business Sector)
- isp: String (Internet Service Provider)
- vendor: String (Device Manufacturer)
- type: String (Device Type)
- critical: Boolean (If scan is targeting critical infrastructure)
- port: Integer (Scanned Open Port)
- criticalTag: String (Critical Infrastructure Targets)

#### /api/ddos
- ip: IP address or IP range using slash notation
- startDate: “yyyy-mm-dd hh:mm:ss.s” format
- endDate: “yyyy-mm-dd hh:mm:ss.s” format
- label: “IoT” or “Desktop”
- country: String
- state: String
- city: String
- org: String (WHOIS Organization)
- isp: String (Internet Service Provider)
- vendor: String (Device Manufacturer)
- type: String (Device Type)
- port: Integer (Scanned Open Port)
- attackType: “ICMP_FLOOD”, “TCP_FLOOD” or “UDP_FLOOD”

## Examples
__All examples are written using cURL__

Get all IoT scans:
```
curl -L -g -X GET 'X.X.X.X:5000/api/scans?user=[USER]&pass=[PASS]' \
-H 'Content-Type: text/plain' \
--data-raw 'label:IoT'
```

Get all IoT scans in the United States on December 10, 2020:
```
curl -L -g -X GET 'X.X.X.X:5000/api/scans?user=[USER]&pass=[PASS]' \
-H 'Content-Type: text/plain' \
--data-raw 'label:IoT AND country:"United States" AND startDate:"2020-12-10" AND endDate:"2020-12-11"'
```

Get all scans in Texas (United States) that target port 80:
```
curl -L -g -X GET 'X.X.X.X:5000/api/scans?user=[USER]&pass=[PASS]' \
-H 'Content-Type: text/plain' \
--data-raw 'label:IoT AND country:"United States" AND state:Texas AND port:80'
```

## Contact
Please direct any questions, comments, concerns or requests for authentication credentials to <eiotsubmission@gmail.com>
