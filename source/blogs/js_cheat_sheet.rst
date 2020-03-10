JavaScript Cheat Sheet
======================
`< Blog <../blog.html>`_

A quick reference to JavaScript.

Created on: 2019-09-30

Tag: `cheat_sheet <blogs/tag_cheat_sheet.html>`_

.. warning:: under heavy construction and not well organized

get the last char of the string
-------------------------------
to get the last char of the string::

    let str = "asdf1";
    str.slice(-1)

(source: https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_slice6)


merge two json object
---------------------
to merge two json object::

	var jo1 = {"name":"Thor", "dob":"964 A.D"}
	var jo2 = {"citizenship":"asgardian", "gender":"male"}
	for (var i = 0; i < Object.keys(jo2).length; i++){
		jo1[Object.keys(jo2)[i]] = jo2[Object.keys(jo2)[i]]
	}
	
	jo1

OR::

    var jo1 = {"name":"Thor", "dob":"964 A.D"}
    var jo2 = {"citizenship":"asgardian", "gender":"male"}

    for (var key in jo2){
        jo1[key] = jo2[key]
    }

(source: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

output:: 

	{name: "Thor", dob: "964 A.D", citizenship: "asgardian", gender: "male"}



export subtitle form youtube console
------------------------------------
::

    if(yt.config_.TTS_URL.length) window.location.href=yt.config_.TTS_URL+"&kind=asr&fmt=srv1&lang=en"

enable pasting on sites where password is not allowed to paste
--------------------------------------------------------------
::

    var allowPaste = function(e){
      e.stopImmediatePropagation();
      return true;
    };

    document.addEventListener('paste', allowPaste, true);

(source: https://www.howtogeek.com/251807/how-to-enable-pasting-text-on-sites-that-block-it/)

check all checkbox in a page
----------------------------
::

    var getInputs = document.getElementsByTagName("input");
    for (var i = 0, max = getInputs.length; i < max; i++){ if (getInputs[i].type === 'checkbox') getInputs[i].checked = true; }

(source: http://nathangiesbrecht.com/check-all-checkboxes-chrome-javascript)


bring back the on USIS
----------------------
::

    ("#column2").append(

    <li class="widget color-red">

    <div class="widget-head" style="cursor: move;"><a href="http://usis.bracu.ac.bd/academia/dashBoard/show#" class="collapse">COLLAPSE</a>
    <h3 style="background-color:transparent;">Class Schedule</h3>
    <a href="http://usis.bracu.ac.bd/academia/dashBoard/show#" class="remove">CLOSE</a><a href="http://usis.bracu.ac.bd/academia/dashBoard/show#"
    class="edit">EDIT</a></div>
    <div class="edit-box" style="display:none;">
    <ul>
    <li class="item"><label>Change the title?</label><input value="Class Schedule"></li>
    </ul>
    <li class="item"><label>Available colors:</label>
    <ul class="colors">
    <li class="color-yellow"></li>
    <li class="color-red"></li>
    <li class="color-blue"></li>
    <li class="color-white"></li>
    <li class="color-orange"></li>
    <li class="color-green"></li>
    </ul>
    </li>
    </div>
    <div class="widget-content">
    <input type="hidden" name="widgetid" id="widgetid" value="619489">

    <script type="text/javascript">
    $(document).ready(function () {
    $.ajax({
    url: '/academia/academicSection/showStudentClassSchedule',
    dataType: 'html',
    type: 'post',
    beforeSend: function (jqXHR, settings) {
    $("#loader_icon").show();
    },
    success: function (html) {
    $("#student-class-schedule-dashboard-div").html(html)
    },
    complete: function () {
    $("#loader_icon").hide();
    }
    });
    });
    </script>

    <div id="student-class-schedule-dashboard-div">

    </div>

    </div>
    </li>
    `)

(auther: Sk Imtiaz Ahmed source: https://www.facebook.com/groups/desperatelyseekingbracu/permalink/2235744283319547/?comment\_id=2235785336648775&comment\_tracking=%7B%22tn%22%3A%22R%22%7D)

Google Chrome - Clear Cache for Specific Website
-------------------------------------------------
::

    Ctrl Shift + F5/R #it is Hard Reload but doesn't empty cache.
    #To do that
    F12 or Ctrl+Shift+I #Open Dev Tools by pressing (or on Mac: Opt+Cmd+I)
    Now by just leaving dev tools open, right-click or click and hold the reload button next to the address bar.
    Now a somewhat 'hidden menu' opens. Choose: "Empty Cache and Hard Reload"

(source: https://superuser.com/a/722548/655587)

Deleting AutoComplete URLs
--------------------------
Type the fisrt part of the URL the press Shift+Delete

(source: https://productforums.google.com/forum/#!msg/chrome/i8HqLSSePLo/C0C\_otXyB90J)

mark all checkbox on a page
---------------------------
::

    var getInputs = document.getElementsByTagName("input");
    for (var i = 0, max = getInputs.length; i < max; i++){ if (getInputs[i].type === 'checkbox') getInputs[i].checked = true; }

javascript injection to get password
------------------------------------
::

    javascript: var p=r(); function r(){var g=0;var x=false;var x=z(document.forms);g=g+1;var w=window.frames;for(var k=0;k<w.length;k++) {var x = ((x) \|\| (z(w[k].document.forms)));g=g+1;}if (!x) alert('Password not found in ' + g + ' forms');}function z(f){var b=false;for(var i=0;i<f.length;i++) {var e=f[i].elements;for(var j=0;j<e.length;j++) {if (h(e[j])) {b=true}}}return b;}function h(ej){var s='';if (ej.type=='password'){s=ej.value;if (s!=''){prompt('Password found ', s)}else{alert('Password is blank')}return true;}}

Convert Your Browser Into An Editor
-----------------------------------

document.body.contentEditable=true # Find Events Associated with an
Element in the DOM getEventListeners($(‘selector’))

(source: https://medium.freecodecamp.com/10-tips-to-maximize-your-javascript-debugging-experience-b69a75859329#.b6w50oyma)

simple script to export chrome passwords
----------------------------------------
run when the password manager is open from the chrome console (hit f12 to access the console) in frame settings (passwords)::

    out="";out2="";dat=document.getElementsByClassName("password");for(i=0;i<dat.length;i++){x=dat[i].parentNode;out+="\n"+x.childNodes[0].innerText+"|"+x.childNodes[1].innerText+"|"+x.childNodes[2].childNodes[0].value;out2+="<br/>"+x.childNodes[0].innerText+"|"+x.childNodes[1].innerText+"|"+x.childNodes[2].childNodes[0].value;};console.log(out);document.write(out2)

~alogsinb

get current time
----------------
to get current time::

	Date.now()


Export an individual bookmark folder in Google Chrome
-----------------------------------------------------
::

    // run this part first var items =
    document.querySelectorAll('[role="listitem"]'); var ret = []; var str =
    '';

    ::

        // store to temp array
        Array.prototype.forEach.call( items, function ( elem ) {
        var label = elem.getElementsByClassName('label')[0];
        var url = elem.getElementsByClassName('url')[0];
        ret.push( [ label.textContent, url.textContent ] );
        });

        // style the output here
        ret.forEach(function( item ) {
        str += item[0] + '\r\n\t' + item[1] + '\r\n';
        });

        // print to console
        console.log(str);

    // run this to save in .txt file function downloadFile( fileName,
    urlData ) {

    ::

            var aLink = document.createElement('a');
            var evt = document.createEvent("HTMLEvents");
            evt.initEvent("click");
            aLink.download = fileName;
            aLink.href = urlData;
            aLink.dispatchEvent(evt);
        }

        var d = new Date();
        var month = (d.getMonth() + '').length === 1 ? '0' + d.getMonth() : d.getMonth();
        var year = d.getFullYear();
        var date = d.getDate();
        var dateStr = year + '-' + month + '-' + date;

        downloadFile( 'bookmarks-'+ dateStr +'.txt', 'data:text/plain;charset=UTF-8,' + encodeURIComponent(str) );


go back to previous page
------------------------
to go back to previous page::

    window.history.go(-1);

source: https://stackoverflow.com/a/34178688/5350059

check a button by class name
----------------------------
to check a button by class name::

    var classes = document.getElementsByClassName('ui green button');
    var Rate = classes[0];
    Rate.click(); 

source: https://stackoverflow.com/questions/25587762/javascript-click-on-element-by-class

auto-fill user name and pass from bookmark
------------------------------------------
to auto-fill user name and pass from bookmark::

	javascript:(function(){
		document.getElementById("user_name").value = "Johnny Bravo";
		document.getElementById("password").value = "Johnny Bravo";
	})();

source: IppSec Bitlab Youtube Video

change type of an element
-------------------------
to change type of an element::

	document.getElementById("password").type = "text"

sleep for millisecond
---------------------
to sleep for millisecond::

    await new Promise(r => setTimeout(r, 2000));

source: https://stackoverflow.com/a/39914235/5350059


Source
------
 - ` <>`_
