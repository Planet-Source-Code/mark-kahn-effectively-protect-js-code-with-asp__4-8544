<div align="center">

## Effectively protect \.js code with asp


</div>

### Description

This uses the asp http_referer variable, some no caching techniques and some other optional methods to make it very hard for most people to view your javascript source code.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Mark Kahn](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/mark-kahn.md)
**Level**          |Intermediate
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |ASP \(Active Server Pages\)
**Category**       |[Security](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/security__4-14.md)
**World**          |[ASP / VbScript](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/asp-vbscript.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/mark-kahn-effectively-protect-js-code-with-asp__4-8544/archive/master.zip)





### Source Code

<style>
.CM{ /*Comments*/
	color	= #008000;
}
.QT{ /*Quotes*/
	color	= #FF00FF;
}
.RW{ /*VBScript/ASP 5.5 reserved Words*/
	color	= #0000FF;
}
.FN{ /*VBScript/ASP 5.5 Functions*/
	color	= #FF0000;
}
.OB{ /*VBScript/ASP 5.5 Objects*/
	color	= #008080;
}
.ME{ /*VBScript/ASP 5.5 Methods/Properties/Objects*/
	color	= #808000;
}
.CN{ /*VBScript/ASP 5.5 Constants*/
	color	= #800000;
}
.ST{	/*Opening and closing script tags*/
	background-color:	#FFFF00;
	color:				#000000;
}
TD{
	font-family:	"Courier New", Courier;
	font-size:		12px;
}
</style>
The idea is pretty simple. If request.servervariables("HTTP_REFERER") doesn't come from the same domain as the script is in, either a) don't show the script or b) show them a fake script. Basically what you're going to need to do is rename your .js files that you want to protect to .asp files and drop in the below code at the top of this file. All the no-cache stuff is so they can't open their temporary internet files and just view the source.<br /><br />Currently, the only way I know of to view the source of a page protected with this method is to use javascript in the URL to change an existing URL on the page. ie: javascript:document.links[0].href='yourjavascriptfile.asp'; and then clicking on that link. But how many users are going to know how to do that? And for the ones that do, see the optional protection below.
<table border=0><tr><td align=right>1 <br>2 <br>3 <br>4 <br>5 <br>6 <br>7 <br>8 <br>9 <br>10 <br>11 <br></td><td><nobr><span class="ST">&lt;%</span><br><span class="OB">response</span>.expires           = <span class="FN">now</span>() - 1<br><span class="OB">Response</span>.ExpiresAbsolute   = <span class="FN">Now</span>() - 1<br><span class="OB">Response</span>.AddHeader         <span class="QT">"Pragma"</span>, <span class="QT">"No-Cache"</span><br><span class="OB">Response</span>.AddHeader         <span class="QT">"cache-control"</span>,<span class="QT">"private"</span><br><span class="OB">Response</span>.CacheControl      = <span class="QT">"no-cache"</span><br><br><span class="RW">if</span> <span class="FN">lcase</span>(<span class="OB">request</span>.servervariables(<span class="QT">"HTTP_REFERER"</span>)) &lt;&gt; <span class="QT">"http://www.cwolves.com/testing/getmysource.asp"</span> <span class="RW">then</span><br>   <span class="CM">' either do a response.end here or write out some fake javascript to fool people</span><br><span class="RW">end</span> <span class="RW">if</span><br><span class="ST">%&gt;</span><br></nobr></td></tr></table>
<table border=0><tr><th colspan="2">Other Optional Methods</th></tr><tr><th nowrap>Allow one-time-access</td><td>This method involves setting a session var, a cookie, or the querystring requesting the javascript file to a random number. On the javascript file, check to see if the number is the same, and then erase it. This provides one-time access to the javascript file meaning if the user tried the above work-around, it still wouldn't work. Still not 100% foolproof though. The user is still capable of opening JUST your html page and then the javascript file manually.</td></tr><tr><th nowrap>Restricting how long the<br />javascript can be accessed for.</th><td>This one is kinda dangerous because it might cause users on slow connections, or javascript files on large pages to not be loaded. Not sure on a complete fix for that yet. Put simply, you set another session var to the current datetime in the page calling the javascript file. Then in the javascript file itself, you just check if it's been more than X seconds since that variable was set. IE in my sample file, I have that variable set to 3 seconds, so anyone trying the above methods to view the script wouldn't be able to after a mere 3 seconds.</td></tr></table>
<br /><br />
Once again, this is by no means foolproof, but it will keep anyone who isn't a fairly decent programmer/designer/developer/whatever from viewing your source code. If you want to see a live example of how this protection works, please take a look at http://www.cwolves.com/testing/getmysource.asp
<br /><br />
HTH.
<br />
-Mark

