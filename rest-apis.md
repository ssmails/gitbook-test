---
description: >-
  This section documents all the externally exposed Cutlass APIs. The APIs can
  be accessed when the Rest-API is running locally or when it is run as part of
  the Kubernetes cluster on AWS.
---

# Rest APIs

The Rest-API Service supports secure access. When using the secure mode the appropriate headers must be provided.

When running locally- Use the local Ip and port that the Rest Service is running on.

Eg http://127.0.0.1:8011/

When running as part of the cluster, Use the ingress Address. The ingress address can be obtained by  running the command \[kubectl get ingress\] and using the ADDRESS field from it. 

Eg: https://paaspreprod-devdevxcmdbapi-3894-608780858.us-west-2.elb.amazonaws.com/

{% api-method method="get" host="https://" path=":ingress/health" %}
{% api-method-summary %}
Get status of Cutlass Service
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="health" type="string" required=true %}
Gives health status for the Rest-API
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Request was successful. Return the result in JSON format.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Request failed as Rest-API Service was not accessible.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://:ingress/v1/query?" path="attribute=value\[&attribute=value\]" %}
{% api-method-summary %}
Get Query Results based on a key-value query
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows the user to get the query results from Dgraph for a match if the provided attributes and values.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="/v1/query" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="attribute=value" type="string" required=true %}
Attribute name and the value to be matched in dgraph
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Request was successful. Return the result in JSON format.
{% endapi-method-response-example-description %}

```
{
	"objects": [{
		"clustername": "",
		"ip": "100.107.8.104",
		"k8sobj": "",
		"name": "webapp-deployment-4-7495658878-nflv5",
		"objtype": "Pod",
		"resourceversion": "",
		"starttime": "2018-10-18 14:36:34 -0700 PDT",
		"status": "Running",
		"uid": "0xea67"
	}]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Request failed as Rest-API Service was not accessible.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://:ingress" path="/v1/query?keyword=\"\"" %}
{% api-method-summary %}
Get Query Results based on a keyword query
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows the user to get the query results from Dgraph for a case-insensitive substring match for the provided keyword.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="/v1/query" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="keyword" type="string" required=true %}
Keyword to be searched in dgraph.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Request was successful. Return the result in JSON format.
{% endapi-method-response-example-description %}

```
{
	"obj17": [{
		"assetid": "987654321",
		"awsacctnumber": "1911-6338-0763",
		"awsregion": "us-west-1",
		"name": "webapp cluster",
		"objtype": "k8s_cluster",
		"resourceversion": "v1",
		"teamid": "123456789",
		"uid": "0x15fcf"
	}, {
		"assetid": "987654321",
		"awsacctnumber": "1911-6338-0763",
		"awsregion": "us-west-1",
		"name": "webapp cluster",
		"objtype": "k8s_cluster",
		"resourceversion": "v1",
		"teamid": "123456789",
		"uid": "0x15ff0"
	}]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Request failed as Rest-API Service was not accessible.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://:ingress" path="/v1/entity/:type/:uid" %}
{% api-method-summary %}
Get Entity Details by uid
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows the user to get details for the provided kubernetes entitity in dgraph.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="/v1/entity" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="TODO" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="type" type="string" required=true %}
Type of entity \[Namespace, Service, Deployment, ReplicaSet, Pod, PersistentVolume, StatefulSet, DaemonSet\]
{% endapi-method-parameter %}

{% api-method-parameter name="uid" type="string" required=true %}
Dgraph uid for the entity
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Request was successful. Return the result in JSON format.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



