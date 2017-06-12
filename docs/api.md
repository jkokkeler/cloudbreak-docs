# API Documentation

 Cloudbreak is a RESTful application development platform whose goal is to help developers deploy HDP clusters in different environments. Once Cloudbreak is deployed in your favorite servlet container, it exposes a REST API, allowing you to spin up Hadoop clusters of any size with your chosen cloud provider.

The [API documentation](https://app.swaggerhub.com/api/Cloudbreak/Cloudbreak/1.14.0) was generated from the code using [Swagger](http://swagger.io/).

## API Authorization

When using the REST interface of Cloudbreak, a user must authenticate using username and password. For a web-application, the exmaple is given in the source, for a stand-alone application, use the following example to get a token.

Authentication end-point: `https://$HOST/identity/oauth/authorize?reposone_type=token&client_id=cloudbreak_shell&scope.0=openid&source=login&redirect_uri=http://cloudbreak.shell`
HTTP POST call with header: `accept: application:x-www-from-urlencoded`
With data: `credential={"username":"'$USERNAME'", "password":"'$PASSWORD'"}`

$HOST Hostname of the host which runs the indentity provider
$USERNAME Username of
$PASSWORD

Example token curl call: `export $TOKEN=$(curl -k -s -iX POST -H "accept: application/x-www-form-urlencoded" -d 'credentials={"username":"'$USERNAME'","password":"'$PASSWORD'"}' "https://$HOST/identity/oauth/authorize?response_type=token&client_id=cloudbreak_shell&scope.0=openid&source=login&redirect_uri=http://cloudbreak.shell" | grep Location | cut -d'=' -f 3 | cut -d'&' -f 1)`

After getting token, example info curl  call: `curl "https://$HOST/cb/api/v1/stacks/$STACKID" -H "Authorization: Bearer $TOKEN"`
