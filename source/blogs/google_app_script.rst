Google App Script Cheat Sheet
=============================
A quick reference to Google App Script.

I have been using Google App Script for quick hack and automation for sometime now. Though it would be easy to record the reusable parts.

sha512 hash of a string
-----------------------
to make a sha512 hash of a string::

    Utilities.base64EncodeWebSafe(Utilities.computeDigest(Utilities.DigestAlgorithm.SHA_512, 'string'))

filter range where string exist
-------------------------------
to filter range where string exist::

    sheet.getRange(coupon_column).getValues().filter(String)

we can find the length with ``.length`` method::

    sheet.getRange(coupon_column).getValues().filter(String)..length

receive GET and POST request
----------------------------
to receive GET and POST request::

    function doGet(e){
        return main(e)
    }

    function doPost(e) {
        return ContentService.createTextOutput('Error!!! POST method not allowed.').setMimeType(ContentService.MimeType.TEXT); 
    }

return data as json
-------------------
to return data as json::

    return ContentService.createTextOutput(JSON.stringify({"key":"value"})).setMimeType(ContentService.MimeType.JSON;

return data as text
-------------------
to return data as text::

    return ContentService.createTextOutput('Error!!! POST method not allowed.').setMimeType(ContentService.MimeType.TEXT);



retrieve post data
------------------
to retrieve post data [1]_::

    var post_data = e.postData.contents // where `e` is event


append row to Google Sheet
--------------------------
to append row to a Google Sheet [2]_::

    sheet.appendRow([data,data]) //must be a array

get sheet by index
------------------
to get sheet by index [3]_::

    var sheet = sheet.getSheets()[index];

get sheet by name
-----------------
to get sheet by name [4]_::

    var sheet = sheet.getSheetByName($sheet_name);

parse json from string
----------------------
to parse json from string::

    var json_parsed = JSON.parse(response)

sent request
------------
to sent request [5]_::

	var url = "https://example.com"

	var data = {"key1":"value","key2":"value"}

	options = {
		"method": "post",
		"headers": {},
		"payload": data};

	var response = UrlFetchApp.fetch(url, options);

retrieve URL encoded params
---------------------------
to retrieve URL encoded params::

	var params = e.parameter //where e is event


get sheet by sheet id
---------------------
to get sheet by sheet idi [6]_::

    var sheet_id = "1vq-rgLqnWQm-WD1eDwdALCNPrY86g27AT--QJ6CIxPY";
    var open_sheet = SpreadsheetApp.openById(sheet_id);
     
print log
---------
to print log [7]_::

    Logger.log($string_in_quote_or_var);



Source
------

.. [1] `How to take data in google sheet script via POST request in JSON format? <https://stackoverflow.com/a/53018010/5350059>`_
.. [2] `appendRow | Class Sheet | Apps Script | Google Devlopers <https://developers.google.com/apps-script/reference/spreadsheet/sheet#appendrowrowcontents>`_
.. [3] `getSheets | Class Spreadsheet | Apps Script | Google Devlopers <https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getsheets>`_
.. [4] `getSheetByName | Class Spreadsheet | Apps Script | Google Devlopers <https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getsheetbynamename>`_
.. [5] `Google Apps Script make HTTP POST <https://stackoverflow.com/a/14764242/5350059>`_
.. [6] `openById | Class Spreadsheet | Apps Script | Google Devlopers <https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#openbyidid>`_
.. [7] `log | Class Logger | Apps Script | Google Devlopers <https://developers.google.com/apps-script/reference/base/logger#logdata>`_



