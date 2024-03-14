# Opensearch-Upgrading-v2.12.0

This Documentation  will discribe HowTo upgrade from Opensearch-v2.11.1 to v2.12.0.

Open the environement file.

```
vi /etc/environment
```

Add the following line to the file. This is for the Admin password that is needed for version 2.12.0.

```
OPENSEARCH_INITIAL_ADMIN_PASSWORD=PasswordHoward123!
```
Log out of the current session and back in again.

```
exit
```

Download new Opensearch & Opensearch -Dashboards packages.

```
wget https://artifacts.opensearch.org/releases/bundle/opensearch/2.12.0/opensearch-2.12.0-linux-x64.deb
```
```
wget https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/2.12.0/opensearch-dashboards-2.12.0-linux-x64.deb
```

Stop both Services

```
systemctl stop opensearch opensearch-dashboards
```

Check status to ensure there stopped.

```
systemctl status opensearch opensearch-dashboards
```

## Install Opensearch

```
sudo dpkg -i opensearch-2.12.0-linux-x64.deb
```

When asked select "N" to keep original files.

Reload SystemD

```
sudo systemctl daemon-reload
```
Start Opensearch

```
sudo systemctl start opensearch
```

Check the Status. 

```
systemctl status opensearch
```

Check the API connection using the password from the environment that was configured above. This will ensure it works.

```
curl https://opensearch.hungry-howard.com:9200 -u admin:'P@$$word!@#123' -k
```

Before continuing fix any isssues.

## Install Opensearch-Dashboards

```
sudo dpkg -i opensearch-dashboards-2.12.0-linux-x64.deb
```

When asked select "N" to keep original files.

Reload systemd
```
sudo systemctl daemon-reload
```

Start Opensearch-Dashboards

```
sudo systemctl start opensearch-dashboards.service
```

Check the Status.

```
sudo systemctl status opensearch-dashboards
```

## SSO Session Logging off Error

If you recieved a 404 error.

```
{"statusCode":404,"error":"Not Found","message":"Not Found"}
```

### FIX:

NOTE: After upgrading opensearch-dashboards, the file (routes.js) will get written over.

When Logging out from your SSO connection and error might occur, the following file will need to be adjusted.

```
vi /usr/share/opensearch-dashboards/plugins/securityDashboards/server/auth/types/saml/routes.js
```

Commented out this line.

```
//  const redirectUrl = authInfo.sso_logout_url || this.coreSetup.http.basePath.serverBasePath || '/';
```

Added this line.

```
const redirectUrl = `${this.coreSetup.http.basePath.serverBasePath}/app/home`;
```

Restart Opensearch-dashboards service.

```
systemctl restart opensearch-dashboards
```

Check the status.

```
systemctl status opensearch-dashboards
```
