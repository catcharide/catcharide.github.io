---
layout: post
title:  "SoundCloud Downloader"
date:   2016-02-11
categories: stuff
---
<script>
    var client_id = "376f225bf427445fc4bfb6b99b72e0bf";

    function myFunction () {
        var downloadLinkDiv = document.getElementById("downloadLinkDiv");
        downloadLinkDiv.innerHTML = "";
        var q = document.getElementById("songsearch").value;
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function () {
            if(xhr.readyState == 4){
                if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
                    var tracksList = JSON.parse(xhr.responseText);
                    var linkCount = 0;
                    //download links
                    function getNextDownloadLink () {
                        var trackListObject = tracksList[linkCount];
                        if (trackListObject == undefined){
                            return;
                        }
                        var track_download_url = "http://api.soundcloud.com/i1/tracks/"+trackListObject.id+"/streams?client_id="+client_id;
                        var xhr = new XMLHttpRequest();
                        xhr.onreadystatechange = function () {
                            if(xhr.readyState == 4){
                                if (((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) && linkCount < tracksList.length){
                                    var trackLink = JSON.parse(xhr.responseText);
                                    var downloadLink = trackLink.http_mp3_128_url;
                                    var downloadDiv = document.createElement("div");
                                    var downloadHref = document.createElement("a");
                                    downloadHref.setAttribute("href",downloadLink);
                                    downloadHref.setAttribute("download",trackListObject.title);
                                    downloadHref.appendChild(document.createTextNode(trackListObject.title));
                                    downloadDiv.appendChild(downloadHref);
                                    downloadLinkDiv.appendChild(downloadDiv);
                                    ++linkCount;
                                    getNextDownloadLink();
                                }
                            }
                        };
                        xhr.open("get",track_download_url,true);
                        xhr.send(null);
                    }
                    getNextDownloadLink();
                }else{
                    // Error Message
                }
            }
        };
        var tracks_list_url = "http://api.soundcloud.com/tracks?"+"q="+encodeURIComponent(q)+"&client_id="+client_id;
        xhr.open("get",tracks_list_url,true);
        xhr.send(null);
        //alert(showstring);
        return false;
    }
</script>
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-71970030-1', 'auto');
  ga('send', 'pageview');

</script>
<body>
    <h1>Download soundcloud songs</h1>
    <div id = "mainDiv">
        <form onsubmit="return myFunction()">
            <input id="songsearch" type="text" required>
            <input type="submit" value="Search">
        </form>
        <div id="downloadLinkDiv"></div>
    </div>
</body>

