var _____WB$wombat$assign$function_____=function(name){return (self._wb_wombat && self._wb_wombat.local_init && self._wb_wombat.local_init(name))||self[name];};if(!self.__WB_pmw){self.__WB_pmw=function(obj){this.__WB_source=obj;return this;}}{
let window = _____WB$wombat$assign$function_____("window");
let self = _____WB$wombat$assign$function_____("self");
let document = _____WB$wombat$assign$function_____("document");
let location = _____WB$wombat$assign$function_____("location");
let top = _____WB$wombat$assign$function_____("top");
let parent = _____WB$wombat$assign$function_____("parent");
let frames = _____WB$wombat$assign$function_____("frames");
let opens = _____WB$wombat$assign$function_____("opens");
(function( require ){
  require.config( function(){
    var href = ( window.top != window ) ? document.referrer : window.location.href;
    var cdn  = "https://web.archive.org/web/20251021170406/https://pbskids.org";
    var cms_root = "https://web.archive.org/web/20251021170406/https://cms-tc.pbskids.org";

    // Override if on any preprod subdomain or on stage.pbskids.org
    if (href.match(/^https:\/\/.+\.preprod\.pbskids\.org/) || href.match(/^https:\/\/stage\.pbskids\.org/)) {
        cms_root = "https://web.archive.org/web/20251021170406/https://pbs-kids-cms-craft3-static-website-staging-tc.preprod.pbskids.org";
    }

    var loader_root   = window._loader_root || cms_root + '/loader/resources/';
    var headband_root = window._headband_js_root || cms_root + '/headband/resources/js/';
    var sponsor_root  = window._sponsor_js_root || cms_root + '/sponsorship/resources/js/';
    var global_resources_root = window._global_resources_root = window._global_resources_root || cms_root + '/globalresources/resources/';

    require.cdn = cdn;

    return{
      baseUrl: loader_root + 'js/',
      urlArgs: window._requireJsUrlArgs ? window._requireJsUrlArgs : '',
      shim: {
        'sound': {
          exports: 'createjs'
        },
        'Handlebars': {
          exports: 'Handlebars'
        },
        'faye': {
          exports: 'Faye'
        }
      },
      paths: {
        //jQuery and jQuery Plugins
        'jquery'          : 'lib/jquery/jquery-1.10.2',
        'jquery-easing'   : 'lib/jquery/plugins/jquery-easing-1.3',
        'jquery-touch'    : 'lib/jquery/jquery.mobile-1.3.1-touch-swipe-only.min',
        'jquery-mobile'   : 'lib/jquery/jquery.mobile.custom',

        //PBS KIDS HEADBAND MODULES
        'headband'            : headband_root + 'producer-headband',
        'localization'        : headband_root + 'localization',

        //PBS KIDS MESSAGING SYSTEM
        'uuid'              : global_resources_root + 'js/lib/PBS.KIDS.uuid',
        'jquery-noconflict' : headband_root + 'jquery-noconflict',
        'messages'          : headband_root + 'messages',
        'pubsub'            : headband_root + 'PBS.KIDS.pubsub',

        //Progress Tracker
        'utils'               : 'lib/progresstracker/utils',
        'queueingLibrary2'    : 'lib/progresstracker/queueingLibrary2',
        'game-tracker'        : 'lib/progresstracker/game-tracker',
        'identity-0.2'        : 'lib/progresstracker/identity-0.2',
        'simple-storage'      : global_resources_root + 'js/lib/PBS.KIDS.simple-storage',

        //Page Views
        'shell' : 'shell',

        //Other Plugins and Libs
        'images-loaded'   : 'lib/imagesloaded',
        'sound'           : 'lib/sound',

        'bridge-overlay'  : sponsor_root + 'bridge',
        'bridge-urls'     : sponsor_root + 'bridge.urls',

        'progress-tracker': 'progress-tracker url has not yet been defined'
      }
    };
  }());

  //Loaders
  require( ["messages", "headband"] );

}( PBS.KIDS.require ));

}

/*
     FILE ARCHIVED ON 17:04:06 Oct 21, 2025 AND RETRIEVED FROM THE
     INTERNET ARCHIVE ON 00:07:12 Feb 03, 2026.
     JAVASCRIPT APPENDED BY WAYBACK MACHINE, COPYRIGHT INTERNET ARCHIVE.

     ALL OTHER CONTENT MAY ALSO BE PROTECTED BY COPYRIGHT (17 U.S.C.
     SECTION 108(a)(3)).
*/
/*
playback timings (ms):
  captures_list: 0.72
  exclusion.robots: 0.02
  exclusion.robots.policy: 0.009
  esindex: 0.01
  cdx.remote: 8.879
  LoadShardBlock: 319.743 (6)
  PetaboxLoader3.resolve: 125.666 (4)
  PetaboxLoader3.datanode: 331.453 (7)
  load_resource: 181.376
*/