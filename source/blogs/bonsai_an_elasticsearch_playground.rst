Bonsai: An Elasticsearch playground
===================================
`< Blog <../blog.html>`_

Experimenting with Elasticsearch using Bonsai.

Created on: 2019-03-15

If you are getting started with Elasticsearch and don't want to setup an Elasticsearch instance, Bonsai is here to rescue. Bonsai is a free Elasticsearch hosting service where we can experiment with Elasticsearch. With the free plan Bonsai provides one cluster with  10k docs, 125MB data, 10 shards and 125MB memory. It may doesn't look a lot but it would definitely give a tailwind on you getting started to Elasticsearch journey.

To get started head over to `Bonsai <https://bonsai.io/>`_ and sign up. Once we get the confirmation mail we can head over to Bonsai and `Log in <https://app.bonsai.io/login>`_.

After successful login we should get redirected to the cluster creation page. There we need to give a name of our cluster, in this case, I am using ``demo_for_blog``. Then we need to choose server region. While choosing the server rescue, keep latency in mind and choose the one closest to your location. We don't have much option when it comes to choosing version and plan as we are using free plan.

Upon successful cluster creation we should see the Overview tab of the cluster. I will give a brief intro of all the tabs on this page.

First we see the Overview page on successful cluster creation. It shows the Status, Region and Elasticsearch Version on top. We should also see ``Launch Kibana`` button on that same row. This page also shows the Cluster Usage and Performance info of last 24 hours.

Then we have Metrics tab. It shows, you got it, different metrics for this cluster like Request Counts, Requests (Counts & Duration), Request Duration Percentiles, Queue time, Concurrency, Bandwidth, Response Codes. The metrics can be seen over the time of 28d, 7d, 1d and 1h. More on how to read the metrics data can be found on `How to read your metrics <https://docs.bonsai.io/article/131-cluster-metrics>`_ doc.

Next to Metrics we have Manage tab. It all about the cluster management and shows info for Current Plan, Current Limits, Update Plan, Trim Logs and Datadog Integration.

The Console tab is quite interesting. It is an interactive web-based UI for interacting with our cluster. Here we can run all the curl equvelent commands to interact with our cluster.

The next tab is Logs which shows log either for Recent Requests or for Top 20 Slow Requests.

The Access tab is where we generate our API token to use it from other application. One of the cons of free plan is there is no read-only access which sucks.

The last tab is Deprovision. When we are done with experimentation, we should deprovision our cluster. We can do that by entering the password for our account and clicking on ``Enter Password to Deprovision`` button.

Just to give an intro we will use our ``demo_for_blog`` cluster and create a new index, update it's mapping, upload 5 data and search for one and update one.

Before we start we will create a generate a new token from the Access tab and use that to perform our operation. Once we enter the name on the Add Credential section and click Generate New Token it should redirected us to a new page where we should see the Access Key and Access Secret for the user. A full URL will also be provided. Keep this 3 things safe. Now if we take a look at the URL is should follow the following schema::

    https://randomuser:randompass@cluster_name-ramdom_number.cluster_region.bonsaisearch.net

For example, I get this full URL::

    https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net

Now we are ready to start playing around.

.. warning:: Most of the commands bellow usages ``curl`` so make sure you have ``curl`` installed. Same results can be achieved using the Console tab as well.

Create an index
---------------
Index in Elasticsearch is much like a table of a database. Let's list all the indexes of our instance::

    curl -XGET "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/_cat/indices?v"

We can see in the following output that we don't have any index as of now.::

    health    status    index    uuid                     pri    rep    docs.count    docs.deleted    store.size    pri.store.size

To create an index name `demo` using ``curl``::

    curl -XPUT "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo?pretty&pretty"

If we are using the Console, we just need to change the verb from the drop down to ``PUT`` and enter index name demo and press enter. In both case, we should see the following message on successful index creation::

    {
      "acknowledged" : true,
      "shards_acknowledged" : true,
      "index" : "demo"
    }

Let's list all the indexes using the same previous command::

    curl -XGET "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/_cat/indices?v"

We can see in the following output that we have created an index named ``demo``::

    health    status    index    uuid                     pri    rep    docs.count    docs.deleted    store.size    pri.store.size
    green     open      demo     wHOxKkbhTxSd1eVG7MWhdw   1      1      0             0               460b          230b


Update Mapping
--------------
Mapping defines how the data will be stored on that table. Let's check the mapping of our index::

    curl -XGET "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/_mapping?pretty&pretty"

We can see from the following output that mapping for our index is not defined.::

    {
      "demo": {
        "mappings": {}
      }
    }

Let's update he mapping our index::

    curl -XPUT "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/_mapping/v1" -H 'Content-Type: application/json' -d'
    {
        "v1": {
          "properties": {
            "name":     { "type": "text"  },
            "age":      { "type": "integer" }
          }
        }
    }'

For the Console just put /demo/_mapping/v1 on the URL input box paste the following in the box bellow and then press enter::

    {
        "v1": {
          "properties": {
            "name":     { "type": "text"  },
            "age":      { "type": "integer" }
          }
        }
    }

In both case we should see the following message::

    {
      "acknowledged": true
    }

Checking the mapping using the same ``curl`` command now shows::

    {
        "demo": {
            "mappings": {
                "v1": {
                    "properties": {
                        "age": {
                            "type": "integer"
                        },
                        "name": {
                            "type": "text"
                        }
                    }
                }
            }
        }
    }

So it seems we have updated our mapping!!!

.. note:: We could have defined the mapping while creating the index but for this blog we choose not to do so.


Uploading Data
--------------
We have defined how to store the data. Now let's upload some::

    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1?pretty&pretty" -H 'Content-Type: application/json' -d' { "name": "user1", "age": 10 }'
    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1?pretty&pretty" -H 'Content-Type: application/json' -d' { "name": "user2", "age": 20 }'
    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1?pretty&pretty" -H 'Content-Type: application/json' -d' { "name": "user3", "age": 30 }'
    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1?pretty&pretty" -H 'Content-Type: application/json' -d' { "name": "user4", "age": 40 }'
    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1?pretty&pretty" -H 'Content-Type: application/json' -d' { "name": "user5", "age": 50 }'

For all successful data upload we should see output similar to this::

    {
      "_index" : "demo",
      "_type" : "v1",
      "_id" : "yZJVfGkBdm4qJtidx0HD",
      "_version" : 1,
      "result" : "created",
      "_shards" : {
        "total" : 2,
        "successful" : 2,
        "failed" : 0
      },
      "_seq_no" : 0,
      "_primary_term" : 1
    }

Searching Data
--------------
Elasticsearch as the name says is used for searching. So let's search the index for ``user2``::

    curl -XGET "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/_search?q=name:user2&pretty&pretty"

We should see this result like this::

    {
        "took": 0,
        "timed_out": false,
        "_shards": {
            "total": 1,
            "successful": 1,
            "skipped": 0,
            "failed": 0
        },
        "hits": {
            "total": 1,
            "max_score": 1.3862944,
            "hits": [
                {
                    "_index": "demo",
                    "_type": "v1",
                    "_id": "pnBWfGkBLqG7BIrR8Z0d",
                    "_score": 1.3862944,
                    "_source": {
                        "name": "user2",
                        "age": 20
                    }
                }
            ]
        }
    }


Update
------
We can update the data stored in the index as well. We will update the age of ``user2`` using two method but for use to update the age of we need to know the ``_id`` of the document. We can use our previous result from search and can see that the ``_id`` is `pnBWfGkBLqG7BIrR8Z0d`. Let's use it to update the age.

1. Fix value. Update a field with a fixed value.::

    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1/pnBWfGkBLqG7BIrR8Z0d/_update" -H 'Content-Type: application/json' -d' { "doc": { "age": 21 } }'

2. Scripted updates. Update a filed with a scripts, in this case the current value of age field and update with 1.::

    curl -XPOST "https://isdrWzc7nq:3MuCsPLpNRU9ofgA4GY@demo-for-blog-6448511871.eu-central-1.bonsaisearch.net/demo/v1/pnBWfGkBLqG7BIrR8Z0d/_update?pretty&pretty" -H 'Content-Type: application/json' -d' { "script" : "ctx._source.age += 1" }'

In both case we should see output like this::

    {
      "_index": "demo",
      "_type": "v1",
      "_id": "pnBWfGkBLqG7BIrR8Z0d",
      "_version": 2,
      "result": "updated",
      "_shards": {
        "total": 2,
        "successful": 2,
        "failed": 0
      },
      "_seq_no": 5,
      "_primary_term": 1
    }

Bonsai and Python
-----------------
We can interact very easily with `Bonsai using Python <https://docs.bonsai.io/article/102-python>`_. But if we need to use bare bone way we can use Python ``requests`` library and use the Access Key and Access Secret as user name and password.::

    import requests
    bonsai_url = "https://demo-for-blog-6448511871.eu-central-1.bonsaisearch.net"
    user_name = "isdrWzc7nq"
    password = "3MuCsPLpNRU9ofgA4GY"
    index = "demo"
    doc_type = "v1"
    id = 1
    field_names = ["name","age"]
    user1 = ["user1",10]
    temp_dict = dict(zip(field_names,user1))
    post_url = bonsai_url + "/" + index + "/" + doc_type + "/" + str(id)
    header = {'Content-type': 'application/json', 'Accept': 'text/plain'}
    post_response = requests.post(post_url, json=temp_dict, headers=header, auth=(user_name, password))
    post_response.status_code #should give 201 if successful
    post_response.content #should give something like this: b'{"_index":"demo","_type":"v1","_id":"1","_version":1,"result":"created","_shards":{"total":2,"successful":2,"failed":0},"_seq_no":8,"_primary_term":1}'


Deprovision Cluster
-------------------
Make sure to deprovision your cluster once you are done.


Source
------
- `Create or update mapping in elasticsearch <https://stackoverflow.com/a/25471930>`_
- `Mapping: Elasticsearch Doc <https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping.html>`_
- `Basic Authentication: Python Requests <http://docs.python-requests.org/en/master/user/authentication/#basic-authentication>`_
- `Bonsai using Python <https://docs.bonsai.io/article/102-python>`_
