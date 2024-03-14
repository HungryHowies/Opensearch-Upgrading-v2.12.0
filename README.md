# Opensearch-Upgrading-v2.12.0

This Documentation  will discribe HowTo upgrade from Opensearch-v2.11.1 to v2.12.0.

Open environement file.

vi /etc/environment

Add the following line to the file. This is for the Admin password needed.

OPENSEARCH_INITIAL_ADMIN_PASSWORD=PasswordHoward123!

Download new packages

wget https://artifacts.opensearch.org/releases/bundle/opensearch/2.12.0/opensearch-2.12.0-linux-x64.deb

wget https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/2.12.0/opensearch-dashboards-2.12.0-linux-x64.deb

Stop Services

systemctl stop opensearch opensearch-dashboards

Check status 

systemctl status opensearch opensearch-dashboards

## Install Opensearch

sudo dpkg -i opensearch-2.12.0-linux-x64.deb

When asked select "N" to keep original files.

sudo systemctl daemon-reload 
  
sudo systemctl start opensearch.service

Check Status. 

systemctl status opensearch

Check connection.

curl https://opensearch.hungry-howard.com:9200 -u admin:'P@$$word!@#123' -k

Mix any isssues before 

## Install Opensearch-Dashboards

sudo dpkg -i opensearch-dashboards-2.12.0-linux-x64.deb

When asked select "N" to keep original files.

sudo systemctl daemon-reload

sudo systemctl start opensearch-dashboards.service

Check Status.
sudo systemctl status opensearch-dashboards

## SSO Session Logging off

When logging off, I recieved a 404 error.

{"statusCode":404,"error":"Not Found","message":"Not Found"}

When Logging out from your SSO connection Logout file will get written over so adjust need to be made
vi /usr/share/opensearch-dashboards/plugins/securityDashboards/server/auth/types/saml/routes.js
systemctl restart opensearch-dashboards
systemctl status opensearch-dashboards













