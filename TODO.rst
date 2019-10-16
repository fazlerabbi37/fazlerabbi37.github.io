TODO
====


.. note:: tasks for markdown_cheat_sheet.rst
.. note:: need to put the css for Strikethrough after every new html convertion 😞
.. note:: add the followings in combo section
.. note:: show the combination of Italics, Bold and Strikethrough like same word itelic, bold and strickthrough and some part itelic, some part bold or some part strickthrough in a sentene later. You can't really make a header bold, but you can italicize certain words. need to show it in combo section. You can add emphasis to link texts. you can make links within headings.
.. note:: resize images to show side by side with the texts
.. note:: add checklist (https://stackoverflow.com/a/31701316/5350059)

----------------------------------------------------------------------

.. note:: task for source/blogs/install_kde_connect_in_ubuntu_18.04.rst
.. note:: indent what is kde connect part

----------------------------------------------------------------------

.. note:: enclose all command line options/args with [] bracket

---------------------------------------------------------------------

.. note:: give api resposne as json and test: return ContentService.createTextOutput('Error!!! POST method not allowed.').setMimeType(ContentService.MimeType.TEXT);

.. note:: get all URL enncoded params as json object: e.parameter where e is event

.. note:: access object data with key: params.first_name

.. note:: sha512 hash of a string: Utilities.base64EncodeWebSafe(Utilities.computeDigest(Utilities.DigestAlgorithm.SHA_512, 'string'))


.. note:: sent request

```
options = {
   "method": "post",
   "headers": {},
   "payload": data};
 var response = UrlFetchApp.fetch(url, options);
```

.. note: convert requet response to json

```
 var json_parsed = JSON.parse(response)
```

.. note:: appendrow: sheet.appendRow([data,data]). must be a array

.. note:: sent data as json in post: e.postData.contents (https://stackoverflow.com/a/53018010/5350059) 
 
.. note:: filter range where string exist: sheet.getRange(coupon_column).getValues().filter(String)

.. 

:: .. note::
