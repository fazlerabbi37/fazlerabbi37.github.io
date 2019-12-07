Elasticsearch Cheat Sheet
=========================
`< Blog <../blog.html>`_

A quick reference to Elasticsearch.

Created on: 2019-01-22

Words wrapped with curly braces, like ``{host}`` are variable, replace them with appropriate value.

List indexes
------------
To list all the indexes of an Elasticsearch instance run the following command [1]_::

    curl -XGET "http://{host}:{port}/_cat/indices?v"

Create an Index
---------------
To create a new index run the following command [2]_::

    curl -XPUT 'http://{host}:{port}/{index}?pretty&pretty'

Delete an Index
---------------
To delete an index run the following command [3]_::

    curl -XDELETE 'http://{host}:{port}/{index}?pretty&pretty'

Upload data
-----------
To upload a single data to an index run the following command [4]_::

    curl -XPUT 'http://{host}:{port}/{index}/{type}/{doc_id}?pretty&pretty' -H 'Content-Type: application/json' -d'
    {
    "field_name": "data"
    }'

Update a field value
--------------------
To update a single data field run the following command [5]_::

    curl -XPOST 'http://{host}:{port}/{index}/{type}/{doc_id}/_update?pretty&pretty' -H 'Content-Type: application/json' -d'
    {
      "doc": { "field_name": "data" }
    }'

    OR

    curl -XPOST 'http://{host}:{port}/{index}/{type}/{doc_id}/_update?pretty&pretty' -H 'Content-Type: application/json' -d'
    {
      "script" : "ctx._source.field_name += 1"
    }'


Search index
------------
To search and index run the following command [6]_::

    curl -XGET 'http://{host}:{port}/{index}/_search?q={field_name}:{keyword}'

Delete index data only
----------------------
To delete only the data of an index run the following command [7]_::

    curl -X POST "http://{host}:{port}/{index}/{type}/_delete_by_query?conflicts=proceed" -H 'Content-Type: application/json' -d'
    {
      "query": {
        "match_all": {}
      }
    }
    '

Source
------
.. [1] `List All Indices <https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-list-indices.html>`_
.. [2] `Create an Index <https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-create-index.html#getting-started-create-index>`_
.. [3] `Delete an Index <https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-delete-index.html#getting-started-delete-index>`_
.. [4] `Indexing/Replacing Documents <https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-modify-data.html#_indexing_replacing_documents>`_
.. [5] `Updating Documents <https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-update-documents.html#getting-started-update-documents>`_
.. [6] `Search <https://www.elastic.co/guide/en/elasticsearch/reference/current/search-search.html#search-search>`_
.. [7] `Delete By Query API <https://www.elastic.co/guide/en/elasticsearch/reference/6.5/docs-delete-by-query.html#docs-delete-by-query>`_
