# Proxy Settings

The below settings will be sent to ESDS for configuration.
Post the configuration the haproxy servers need to be configured to be served via the api.pmccare.in subdomain. That problem can be delegated to PMC IT Team.

| # | Type         | Service              | IP Address    | Port  | Domain        | URL Location          | Proxy Pass URL               |
|---|--------------|----------------------|---------------|-------|---------------|-----------------------|------------------------------|
| 1 | Microservice | Application Config   | 10.10.180.210 | 8007  | api.pmccare.in| /appConfiguration/v1/ | http://10.10.180.210:8007/v1/ |
| 2 | Microservice | info                 | 10.10.180.210 | 8002  | api.pmccare.in| /info/v1/             | http://10.10.180.210:8002/v1/ |
| 3 | Microservice | Image Proxy          | 10.10.180.210 | 12701 | api.pmccare.in| /image/v1/            | http://10.10.180.210:12701/v1/|
| 4 | Microservice | Near Me              | 10.10.180.210 | 8004  | api.pmccare.in| /nearMe/v1/           | http://10.10.180.210:8004/v1/ |
| 5 | Microservice | Object Storage       | 10.10.180.210 | 8008  | api.pmccare.in| /objectStorage/v1/    | http://10.10.180.210:8008/v1/ |
| 6 | Microservice | Payment Gateway      | 10.10.180.210 | 15532 | api.pmccare.in| /taxpay/v1/           | http://10.10.180.210:15532/v1/|
| 7 | Microservice | User                 | 10.10.180.210 | 8003  | api.pmccare.in| /user/v1/             | http://10.10.180.210:8003/v1/ |
| 8 | Microservice | User Authentication  | 10.10.180.210 | 8005  | api.pmccare.in| /authenticationConfiguration/v1/| http://10.10.180.210:8005/v1/ |
| 9 | Microservice | User Engagement      | 10.10.180.210 | 8006  | api.pmccare.in| /userEngagement/v1/   | http://10.10.180.210:8006/v1/ |
