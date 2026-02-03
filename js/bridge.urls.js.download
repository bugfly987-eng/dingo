var _____WB$wombat$assign$function_____=function(name){return (self._wb_wombat && self._wb_wombat.local_init && self._wb_wombat.local_init(name))||self[name];};if(!self.__WB_pmw){self.__WB_pmw=function(obj){this.__WB_source=obj;return this;}}{
let window = _____WB$wombat$assign$function_____("window");
let self = _____WB$wombat$assign$function_____("self");
let document = _____WB$wombat$assign$function_____("document");
let location = _____WB$wombat$assign$function_____("location");
let top = _____WB$wombat$assign$function_____("top");
let parent = _____WB$wombat$assign$function_____("parent");
let frames = _____WB$wombat$assign$function_____("frames");
let opens = _____WB$wombat$assign$function_____("opens");
(function( require, define, factory ){
  //AMD support for {Global}.requireJS
  if( typeof define === "function" && define.amd ){
    define(factory);
  }
  else{
    factory();
  }
}( PBS.KIDS.require, PBS.KIDS.define, function(){

  var bridgeURLs = function (hostname, pathname) {
    return ( !/^(.+\.)?pbskids\.org$/.test(hostname) )
              && ( pathname.indexOf('/redir/http') == -1 )
              && ( hostname != 'pbskidsgo.org' )
              && ( hostname != 'pbskidsplay.org' )
              && ( hostname != 'www.pbskidsplay.org' )
              && ( hostname != 'dipsy.pbs.org' )
              && ( hostname != 'video.pbs.org' )
              && ( hostname != 'pbskids.local')
              && ( hostname != 'tortuga.dev' )
              && ( hostname != 'tortuga-docker.localhost' )
              && ( hostname.length > 0 || pathname.length > 0 )
              // Relative URLs cause hostname to be blank in IE 8 or lower. These should not cause bridge overlay to appear.
              && ( !(navigator.appName == 'Microsoft Internet Explorer' && hostname.length === 0) )
              && ( pathname.indexOf('openVideoWin') == -1 )
              && ( pathname.indexOf('history.back') == -1 )
              || ( pathname.indexOf('parentsteachers') != -1 )
              || ( pathname.indexOf('caregiver') != -1 )
              || ( pathname.indexOf('itsmylife/parents') != -1 )
              || ( pathname.indexOf('animalia/parents_and_teachers') != -1 )
              || ( pathname.indexOf('parentsTeachers') != -1 )
              || ( pathname.indexOf('mamamirabelle/parents') != -1 )
              || ( pathname.indexOf('barney/pareduc') != -1 )
              || ( pathname.indexOf('zoom/grownups') != -1 )
              || ( pathname.indexOf('readingrainbow/parents_and_teachers') != -1 )
              || ( pathname.indexOf('wordgirl/parentsandteachers') != -1 )
              || ( pathname.indexOf('electriccompany/parentseducators') != -1 )
              || ( pathname.indexOf('wordworld/parentsandteachers') != -1 )
              || ( pathname.indexOf('wordworld/sitemap') != -1 )
              || ( pathname.indexOf('wordworld/contactus') != -1 )
              || ( pathname.indexOf('wordworld/activities') != -1 );
  };//end bridgeURLs()


  var bridgeURLTemplates = function (hostname, pathname, linkClass) {
      if ( (hostname == 'pbsparents.org' || hostname == 'www.pbsparents.org') || ( (hostname == 'pbs.org' || hostname == 'www.pbs.org') && bridgeLinkPathname.substring(0,9) == '/parents/' ) ) { return 'parents'; }
      if ( ( pathname.indexOf('animalia/parents_and_teachers') != -1 ) || ( pathname.indexOf('parentsteachers') != -1 ) || ( pathname.indexOf('itsmylife/parents') != -1 ) || ( pathname.indexOf('readingrainbow/parents_and_teachers') != -1 ) || ( pathname.indexOf('barney/pareduc') != -1 ) || ( pathname.indexOf('grownups') != -1 ) || ( pathname.indexOf('/caregiver') != -1 ) || ( pathname.indexOf('parents') != -1 ) ) { return 'parentsSection'; }
      else if ( hostname == 'pbslearningmedia.org' || hostname == 'www.pbslearningmedia.org' ) { return 'teachers'; }
      else if ( hostname == 'pbs.org' || hostname == 'www.pbs.org') { return 'pbsorg'; }
      else if ( linkClass == 'sponsor-link' ) { return 'sponsor'; }
      else { return 'default'; }
  };//end bridgeURLTemplates()


  var  bridgeCursorFix = function (hostname, pathname) {
    if ( ( pathname.indexOf('teletubbies') != -1 ) ||
      ( pathname.indexOf('sesame') != -1 ) ||
      ( pathname.indexOf('panwapa') != -1 ) ||
      ( pathname.indexOf('mamamirabelle') != -1 ) ||
      ( pathname.indexOf('caillou') != -1 ) ||
      ( pathname.indexOf('toopyandbinoo') != -1 ) ||
      ( pathname.indexOf('/zoom/games/goldburgertogo/') != -1) )
    {
      return true;
    }

    return false;
  };//end bridgeCursorFix()


  var bridgeNoConflict = function (hostname, pathname) {
    if ( ( pathname.indexOf('curiousgeorge') != -1 ) ){
      return true;
    }

    return false;
  };//end bridgeNoConflict()


  //Create Globals
  var exports = ( typeof exports !== 'undefined' ) ? exports : window ;
  exports.bridgeURLs         = bridgeURLs;
  exports.bridgeURLTemplates = bridgeURLTemplates;
  exports.bridgeCursorFix    = bridgeCursorFix;
  exports.bridgeNoConflict   = bridgeNoConflict;

  return (
    "Created : \r\n" +
    "  - window.bridgeURLs() \r\n" +
    "  - window.bridgeURLTemplates() \r\n" +
    "  - window.bridgeCursorFix() \r\n" +
    "  - window.bridgeNoConflict() \r\n"
  );

}));

}

/*
     FILE ARCHIVED ON 15:41:13 Oct 21, 2025 AND RETRIEVED FROM THE
     INTERNET ARCHIVE ON 00:02:05 Feb 03, 2026.
     JAVASCRIPT APPENDED BY WAYBACK MACHINE, COPYRIGHT INTERNET ARCHIVE.

     ALL OTHER CONTENT MAY ALSO BE PROTECTED BY COPYRIGHT (17 U.S.C.
     SECTION 108(a)(3)).
*/
/*
playback timings (ms):
  captures_list: 0.729
  exclusion.robots: 0.023
  exclusion.robots.policy: 0.01
  esindex: 0.012
  cdx.remote: 34.702
  LoadShardBlock: 241.485 (6)
  PetaboxLoader3.datanode: 241.742 (7)
  load_resource: 180.67
  PetaboxLoader3.resolve: 150.368
*/