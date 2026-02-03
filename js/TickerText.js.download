var _____WB$wombat$assign$function_____=function(name){return (self._wb_wombat && self._wb_wombat.local_init && self._wb_wombat.local_init(name))||self[name];};if(!self.__WB_pmw){self.__WB_pmw=function(obj){this.__WB_source=obj;return this;}}{
let window = _____WB$wombat$assign$function_____("window");
let self = _____WB$wombat$assign$function_____("self");
let document = _____WB$wombat$assign$function_____("document");
let location = _____WB$wombat$assign$function_____("location");
let top = _____WB$wombat$assign$function_____("top");
let parent = _____WB$wombat$assign$function_____("parent");
let frames = _____WB$wombat$assign$function_____("frames");
let opens = _____WB$wombat$assign$function_____("opens");
(function (plumlib) {

	var TickerText=function(string) {
		this.initialize(string);
	}

	var tt=TickerText.prototype=new Object;

	
	tt.fulltext;
	tt.windowsize; // size of the window to display the ticker
	tt.textwidth;
	tt.matches;
	tt.startpoints;
	tt.endpoints;
	tt.matches;

	tt.initialize=function(string) {
		this.fulltext=string;
//		this.fulltext="I'm dressed as a potted plant. It's an indoor/outdoor disguise. <span class=\"bold\">Spyhound Agent Ivy</span> * As a Spyhound I'm a chicken dressed as a very small dog. You'll never detect me. <span class=\"agentname\">Spyhound Agent Brock</span> * We will thwart Spot Spotnick if it's the last thing I do. <span class=\"agentname\">Spyhound Agent Ruffs#1 fan</span> * <span class=\"ruffsays\">Thanks Ruffs#1 fan, I can use all the help I can get to defeat my arch enemy. Yours, Ruff</span>";
		this.windowsize=51;
		this.textwidth=this.fulltext.length;
		
		this.matches=new Array;
		this.startpoints=new Array;
		this.endpoints=new Array;
		this.matchpoints=new Array;
		
		var spantag=/<[^>]+>/g;
		var match;
		while (match = spantag.exec(this.fulltext)) {
			this.matches.push(match);
		}
		
		var match = this.fulltext.search(spantag);
		
		for(var m in this.matches) {
		this.matchpoints.push(this.fulltext.search(this.matches[m]));
		if(this.matches[m]!="</span>") {
			this.startpoints.push(this.fulltext.search(this.matches[m])); // these are the points at which each of the tags is found.
		} else {
			this.endpoints.push(this.fulltext.search(this.matches[m]));
		}
		this.fulltext=this.fulltext.replace(this.matches[m],'');
	}

	}


	tt.subticker=function(start,end) {
		var tickerpos=start;
		var numchars=end-start;
		
		// for wrapping around...
/*		if(tickerpos > this.fulltext.length - this.windowsize) {
		var halflength=this.fulltext.length;
		this.fulltext+=" | " + this.fulltext;
		// and add to all of the span arrays also
		var newmatch=matchpoints;
		
		for(var m in newmatch) {
			matchpoints.push(newmatch[m] + halflength + 3);
			matches.push(matches[m]);
		}
	} 
*/

		var tickertext=this.fulltext.substr(tickerpos,numchars);

		var spaces='';

		if(this.fulltext.substr(numchars-1,numchars)!=' ') {
			// go through until finding the next space
			var lasthalf=this.fulltext.substr(numchars,(this.fulltext.length-numchars));
			var wherespace=lasthalf.indexOf(' ');
			if(wherespace<0) {
				wherespace=this.fulltext.length-end;
			}
			while(wherespace>0) {
				wherespace--;
				spaces+='&nbsp;';
			}
		}

		var lastpos=tickerpos + numchars;
		var placethings=new Array;
		var sentencechunks=new Array;
		var pastpos=0;
		var newpos=0;
		var addfirst=-1;
		
		
			for(var m in this.matchpoints) {
		if(this.matchpoints[m] >= tickerpos && this.matchpoints[m] <= lastpos) {
			newpos=this.matchpoints[m]-tickerpos;
			var nm=this.matches[m];
			placethings.push([newpos,nm]);
			sentencechunks.push(tickertext.slice(pastpos,newpos));
			pastpos=this.matchpoints[m]-tickerpos;
			if(placethings.length<2 && this.matches[m]=="</span>") {
				addfirst=m-1;
			}
		} else if(this.matchpoints[m] <= tickerpos) {
		// there's no <span> tag in this particular zone... but check to see whether one would otherwise be open!
		if(this.matches[m]!="</span>") {
			addfirst=m;
		} else {
			addfirst=-1;
		}
	}

	}	
		
	sentencechunks.push(tickertext.slice(pastpos));
	
	
	if(sentencechunks.length > 0) {
	tickertext="";
	if(addfirst > -1) {
		tickertext+=matches[addfirst];	
	}

	var lastthing;	
	for(sc in sentencechunks) {
		tickertext+=sentencechunks[sc];
		if(sc < placethings.length) {
		tickertext+=placethings[sc][1];
//		alert("place " + placethings[sc][1]);
		lastthing=placethings[sc][1];
		}

	}

	tickertext+=spaces;

	if(lastthing!="</span>") {
		tickertext+="</span>";
	}
}
	
//	alert("teak: "  + tickertext);

	// IF SINGLE LINE:
 // replace spaces with &nbsp;?
//	ticker.innerHTML=tickertext;
	tickertext=tickertext.replace(/ /g, "&nbsp;");
	tickertext=tickertext.replace(/<span&nbsp;/g,"<span ");

// MULTILINE: pad with &nbsp;?

	return tickertext;
	
	}
	
	tt.untaggedlength=function() {
		return this.fulltext.length;
	}


TickerText.addBreaks=function(htmltext,charlength) {
	var charl=charlength,
	visiblechar=0,
	breakpoints=new Array,
	lastspace=0,
	tl=htmltext.length,
	inbracket=false;
	
	for(var j=0;j<tl;j++) {
		if(htmltext.charAt(j)=="<") {
			inbracket=true;
		}
		if(htmltext.charAt(j)==" ") {
			lastspace=j;
		}
		if(inbracket) {
			visiblechar--;
		}
		
		if(visiblechar>=charl) {
			breakpoints.push(lastspace);
			charl=lastspace+charlength;
		}
		
		if(htmltext.charAt(j)==">") {
			inbracket=false;
		}
		visiblechar++;
	}

	var newhtmltext=' ';
	var lastbreak=0;
	for(var i=0;i<breakpoints.length;i++) {
		var nextpiece=htmltext.slice(lastbreak,breakpoints[i]);
		newhtmltext+=nextpiece + "<br />";	
		lastbreak=breakpoints[i];
	}
	newhtmltext+=htmltext.slice(lastbreak,htmltext.length);
	return newhtmltext;
}

	plumlib.TickerText=TickerText;


})(plumlib=plumlib || {});

var plumlib;

}

/*
     FILE ARCHIVED ON 17:06:22 Oct 21, 2025 AND RETRIEVED FROM THE
     INTERNET ARCHIVE ON 00:12:31 Feb 03, 2026.
     JAVASCRIPT APPENDED BY WAYBACK MACHINE, COPYRIGHT INTERNET ARCHIVE.

     ALL OTHER CONTENT MAY ALSO BE PROTECTED BY COPYRIGHT (17 U.S.C.
     SECTION 108(a)(3)).
*/
/*
playback timings (ms):
  captures_list: 1.157
  exclusion.robots: 0.052
  exclusion.robots.policy: 0.018
  esindex: 0.028
  cdx.remote: 17.142
  LoadShardBlock: 137.52 (3)
  PetaboxLoader3.datanode: 231.66 (4)
  load_resource: 357.77
  PetaboxLoader3.resolve: 225.872
*/