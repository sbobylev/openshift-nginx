# Sample NGINX OpenShift Template

#### Description ####

This template can be used to deploy a openshift-nginx to OpenShift. It creates several basic obejects such as ImageStream, Service, ConfigMap, DeploymentConfig and Route.

#### Deploying ####

```bash
$> oc new-project helloworld 1> /dev/null

$> oc create -f templates/openshift-template-nginx.yaml
imagestream "openshift-nginx" created
service "openshift-nginx" created
configmap "nginxconf" created
deploymentconfig "openshift-nginx" created
route "openshift-nginx" created
```

#### Verifying ####

```bash
$> oc get -o template dc/openshift-nginx --template={{.status.readyReplicas}}
1%

$> oc get routes
NAME              HOST/PORT                                     PATH      SERVICES          PORT       TERMINATION   WILDCARD
openshift-nginx   openshift-nginx-helloworld.127.0.0.1.nip.io             openshift-nginx   8080-tcp                 None

$> curl -I openshift-nginx-helloworld.127.0.0.1.nip.io
HTTP/1.1 200 OK
Server: nginx/1.13.5
Date: Sun, 26 Nov 2017 22:38:49 GMT
Content-Type: text/html
Content-Length: 612
Last-Modified: Tue, 08 Aug 2017 15:25:00 GMT
ETag: "5989d7cc-264"
Accept-Ranges: bytes
Set-Cookie: eeb35b7ea486a22e60e859dcd6fc711d=8bdd63c9be663ea66fdaaebc6062b59d; path=/; HttpOnly
Cache-control: private
```

####  OpenShift cluster ####

To be able to see all projects via the Web Console, run the following command.

```bash
$> oc adm policy add-cluster-role-to-user cluster-admin system --as=system:admin
```
