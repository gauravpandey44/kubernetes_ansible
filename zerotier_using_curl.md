# Zerotier using Curl


## Create a Network

```
{

curl -H "Authorization: Bearer <API-ACCESS-TOKEN>" -X POST -d '{"config":{"name":"<NETWORK-NAME>","private":true}}' https://my.zerotier.com/api/network

}

```

## Get All Node details


```
{

api="dy9KunbkB11D6kw3RL0aLYzlcnTqVXf8"
network_id="a09acf023378d183"

curl -X GET -H "Content-Type: application/json" -H "Authorization: bearer ${api}" "https://my.zerotier.com/api/network/${network_id}/member" | jq

}

```





## Authorize the node

```
{

api="dy9KunbkB11D6kw3RL0aLYzlcnTqVXf8"
network_id="a09acf023378d183"
nodeid=$(sudo zerotier-cli status | awk '{print $3}')
name="aws"

curl -X POST -H "Content-Type: application/json" -H "Authorization: bearer ${api}" "https://my.zerotier.com/api/network/${network_id}/member/${nodeid}" -d "{\"name\":\"${name}\",\"description\":\"${name}\",\"config\":{\"authorized\":true}}"

}

```
## De-Authorize a node

Hiding a member will deauthorize it and hide it from view. Hidden members can be found by selecting the hidden checkmark in the member list and here can they be unhidden and authorized again (2-click process).

```
{

curl -H "Authorization: Bearer <API-ACCESS-TOKEN>" -X POST -d '{"hidden":true}' https://my.zerotier.com/api/network/<NETWORK-ID>/member/<NODE-ID>

}
```


## Authorizing and setting IP of node

```

{

api="dy9KunbkB11D6kw3RL0aLYzlcnTqVXf8"
network_id="a09acf023378d183"
nodeid=$(sudo zerotier-cli status | awk '{print $3}')
name="aws"

curl -X POST -H "Content-Type: application/json" -H "Authorization: bearer ${api}" "https://my.zerotier.com/api/network/${network_id}/member/${nodeid}" -d "{\"name\":\"${name}\",\"description\":\"${name}\",\"config\":{\"authorized\":true,\"ipAssignments\":[\"192.168.196.176\"]}}"

}

```


