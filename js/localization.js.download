var _____WB$wombat$assign$function_____=function(name){return (self._wb_wombat && self._wb_wombat.local_init && self._wb_wombat.local_init(name))||self[name];};if(!self.__WB_pmw){self.__WB_pmw=function(obj){this.__WB_source=obj;return this;}}{
let window = _____WB$wombat$assign$function_____("window");
let self = _____WB$wombat$assign$function_____("self");
let document = _____WB$wombat$assign$function_____("document");
let location = _____WB$wombat$assign$function_____("location");
let top = _____WB$wombat$assign$function_____("top");
let parent = _____WB$wombat$assign$function_____("parent");
let frames = _____WB$wombat$assign$function_____("frames");
let opens = _____WB$wombat$assign$function_____("opens");
/**
 * PBS KIDS Localization
 *
 * @author Renzo Olguin
 * @email rmolguin@pbs.org
 */
(function() {
  "use strict";
  var require, define;

  if (
    typeof PBS !== "undefined" &&
    PBS.KIDS &&
    PBS.KIDS.require &&
    PBS.KIDS.define
  ) {
    require = PBS.KIDS.require;
    define = PBS.KIDS.define;
  } else {
    require = window.require;
    define = window.define;
  }

  /* DEBUGGING UTILS
  ################################################*/
  // Only debug on subdomains of pbskids.org, e.g. stage.pbskids.org,
  // except NOT on help.pbskids.org.
  var _APP_NAME = "PBS KIDS Localization";
  var _APP_VERS = "1.3.0";
  var _STAGING_SUBDOMAINS = /(^((?!(www|help|cms)(\-tc)?\.).+)pbskids\.org$|tortuga\-docker\.localhost)/;
  var _DEBUG = _STAGING_SUBDOMAINS.test(window.location.hostname)
    ? true
    : false;
  var _log = function(message, args, type, force) {
    if (_DEBUG === true || force === true) {
      if (typeof message === "string" || !!args) {
        message = _APP_NAME + " ver. " + _APP_VERS + " | " + message;
      } else {
        args = message;
        message = _APP_NAME + " ver. " + _APP_VERS + " | ";
      }

      if (typeof console !== "undefined") {
        if (type === "error" && console.error) {
          console.error(message, args);
        } else if (type === "error" && window.Error) {
          throw new Error(message);
        } else if (type === "info" && console.info) {
          console.info(message, args);
        } else if (type === "warn" && console.warn) {
          console.warn(message, args);
        } else if (console.log) {
          console.log(message, args);
        } else if (typeof window.debug !== "undefined") {
          window.debug.log.apply(message, args);
        }
      }
    }
  };

  var _getCookie = function(c_name) {
    if (document.cookie.length > 0) {
      var c_end,
        c_start = document.cookie.indexOf(c_name + "=");
      if (c_start !== -1) {
        c_start = c_start + c_name.length + 1;
        c_end = document.cookie.indexOf(";", c_start);
        if (c_end === -1) {
          c_end = document.cookie.length;
        }
        return decodeURI(document.cookie.substring(c_start, c_end));
      }
    }
    return "";
  };

  var _setCookie = function(c_name, value, exdays, path, domain) {
    var c_value = encodeURI(value);
    var exdate;

    if (exdays !== null) {
      exdate = new Date();
      exdate.setDate(exdate.getDate() + exdays);
      c_value += "; expires=" + exdate.toUTCString();
    }

    if (path !== null) {
      c_value += "; path=" + path;
    }

    if (domain !== null) {
      c_value += "; domain=" + domain;
    }

    document.cookie = c_name + "=" + c_value;
  };

  /* Start Building
  ################################################*/
  (function(require, define, factory) {
    if (typeof define === "function" && define.amd) {
      //Global AMD for requireJS
      define("localization", ["jquery"], factory);
    } else {
      //Assume jQuery is directly loaded via <script/>
      factory(jQuery);
    }
  })(require, define, function($) {
    var _STATION_SERVICES =
      "https://web.archive.org/web/20251021154112/https://station.services.pbs.org/api/public/v1/stations/";
    var _LOCALIZATION_SERVICE =
      "https://web.archive.org/web/20251021154112/https://localization.services.pbs.org/localize/";
    var _autoLocalize = false;

    var dom = typeof exports !== "undefined" ? exports : window;
    dom.org = dom.org || {};
    dom.org.pbskids = dom.org.pbskids || {};

    if (dom.org.pbskids.localization) return dom.org.pbskids.localization;
    var _localization = (dom.org.pbskids.localization = {
      localized: false,
      autoLocalized: false
    });

    var _headband_root = dom._headband_js_root ? dom._headband_js_root + '../' : 'https://web.archive.org/web/20251021154112/https://cms-tc.pbskids.org/headband/resources/';

    _localization.LocalizationEvent =
      _localization.LocalizationEvent ||
      (function() {
        /* Private Properties
      **************************/
        var _EVENT_CLASS = "org_pbskids_localization_LocalizationEvent";

        return {
          /* Public Properties
        **************************/
          /* Event Types */
          ZIPCODE_CHANGE: _EVENT_CLASS + "_ZipcodeChange",
          STATION_CHANGE: _EVENT_CLASS + "_StationChange",
          STATION_LIST_CHANGE: _EVENT_CLASS + "_StationListChange",
          LOCALIZATION_READY: _EVENT_CLASS + "_LocalizationReady",

          /* Public Methods
        **************************/
          dispatchEvent: function(o) {
            var e,
              d = {};
            o.eventType = (o.eventType || "").replace(/\./g, "_");

            switch (o.eventType) {
              case this.ZIPCODE_CHANGE:
                d.zipcode = o.zipcode;
                break;

              case this.STATION_CHANGE:
                d.station = o.station;
                break;

              case this.STATION_LIST_CHANGE:
                d.stations = o.stations;
                break;

              case this.LOCALIZATION_READY:
                //No additional data
                break;

              default:
                return;
            } //end switch

            e = $.Event(o.eventType); // build custom event object
            for (var i in d) e[i] = d[i]; //add custom data to event object
            _log("LocalizationEvent.dispatchEvent", e);
            $(o.caller || document).trigger(e); //fire/dispatch/trigger custom event

            if (
              window.$ &&
              window.$ != $ &&
              window.$.fn &&
              window.$.fn.jquery
            ) {
              //This is to dispatch the event if a producer is using a global
              //version of jQuery which is not the same version used by this class.
              if (typeof window.$(o.caller || document).trigger == "function") {
                window.$(o.caller || document).trigger(e);
              }
            } else if (window.jQuery && window.jQuery != $) {
              if (
                typeof window.jQuery(o.caller || document).trigger == "function"
              ) {
                window.jQuery(o.caller || document).trigger(e);
              }
            }

            if (window.PBSKidsPlayerEvents) {
              PBSKidsPlayerEvents.emit(e.type, e);
            }
          } //dispatchEvent()
        }; //return
      })(); //LocalizationEvent();

    function init() {
      // Add event listeners
      $(document).on(
        _localization.LocalizationEvent.ZIPCODE_CHANGE,
        onZipChange
      );
      $(document).on(
        _localization.LocalizationEvent.STATION_LIST_CHANGE,
        onStationListChange
      );

      //Get root directory
      var __getQuery = (function(a) {
        var i,
          p,
          b = {};
        if (a !== "") {
          for (i = 0; i < a.length; i++) {
            p = a[i].split("=");
            if (p.length > 0)
              b[p[0]] = p[1]
                ? decodeURIComponent(p[1].replace(/\+/g, " "))
                : "";
          }
        }
        return b;
      })(window.location.search.substr(1).split("&"));
      var __href =
        window.top != window ? document.referrer : window.location.href;

      _log(
        "Cookie :: pbskids.autolocalized =",
        _getCookie("pbskids.autolocalized")
      );
      _log("Cookie :: pbs.station =", _getCookie("pbs.station"));
      _log("Cookie :: pbskids.station =", _getCookie("pbskids.station"));

      //Localize to station by the following order of importance:
      // 1) "station" GET var
      // 2) "pbskids.station" COOKIE
      // 3) "pbs.station" COOKIE -- treated as confirmed by user
      // 4) auto-localize based on zip-code (obtained via ip-address)

      //try localizing via GET var.
      if (!_localization.updateStation(__getQuery["station"])) {
        //not localized via GET var, see if station was confirmed before on pbskids.org.
        if (_getCookie("pbskids.autolocalized") == "false") {
          //station has been user confirmed on PBS KIDS, get pbskids.station cookie.
          if (!_localization.updateStation(_getCookie("pbskids.station"))) {
            //actually didn't have pbskids.station cookie, try pbs.station cookie.
            if (!_localization.updateStation(_getCookie("pbs.station"))) {
              //pbs.station cookie does not exist, autolocalize.
              _autoLocalize = true;
            }
          }
        } else {
          //station has not been user confirmed before on pbskids.org, see if confirmed on pbs.org
          if (!_localization.updateStation(_getCookie("pbs.station"))) {
            //pbs.station cookie does not exist, autolocalize.
            _autoLocalize = true;
          }
        }
      }

      _log("Private Var :: _autoLocalize =", _autoLocalize);

      //get zip from cookie if available
      var __zip = _getCookie("pbskids.zipcode");
      if (__zip) {
        updateZip(__zip);
      } else {
        $.ajax({
          // Autolocalize
          url: _LOCALIZATION_SERVICE + "auto/",
          cache: false,
          success: function(data) {
            _log("Auto Localized", data);
            if (data && data.zipcode) {
              updateZip(data.zipcode);
            }
          }
        });
      } //end if _zip

      //let the dom know that this module is ready
      _localization.LocalizationEvent.dispatchEvent({
        eventType: _localization.LocalizationEvent.LOCALIZATION_READY
      });
    } //init()

    function updateZip(zip) {
      zip = zip + "";
      if (!zip.match(/^[0-9]{5}$/)) return;

      _localization.zip = _localization.zipcode = zip;
      _setCookie("pbskids.zipcode", zip, 2 * 365, "/", ".pbskids.org");

      _localization.LocalizationEvent.dispatchEvent({
        eventType: _localization.LocalizationEvent.ZIPCODE_CHANGE,
        zipcode: zip
      });

      _log("Fetch stations for zipcode, " + zip);
      $.ajax({
        url: _LOCALIZATION_SERVICE + "zipcode/" + zip + "/",
        cache: true,
        jsonpCallback: "pbskids_localization_get_callsigns_by_zip",
        success: onStationListLoaded
      });
    }

    /* Event Handlers
    **************************/
    function onStationListLoaded(data) {
      _log("onStationsListLoaded", data);

      // Collect unique flagship stations.
      var __flagship_stations = {};
      var __stationQuery = '';

      for (var i = 0; i < data.stations.length; i++) {

        var __flagship = data.stations[i]["flagship"];

        if (__flagship_stations[__flagship]) {
          continue;
        }

        __flagship_stations[__flagship] = {
          callLetters: __flagship,
          sortPosition: i // Preserve station sorting order.
        };

        // Build query to collect flagship station data.
        __stationQuery += (__stationQuery === '' ? '?' : '&') + 'call_sign=' + __flagship;
      }

      console.log('Stations by zipcode lookup:', {'__flagship_stations': __flagship_stations});


      // Get metadata and logo urls for each of the available flagship stations.
      $.ajax({
        url: _STATION_SERVICES + __stationQuery,
        dataType: "json",
        success: function(response) {
          _localization.stations = response.data.map(function(stationData) {
            // Expose just the station data.
            stationData = stationData.attributes;

            // Backfill the sort position obtained when searching by zipcode.
            stationData['sortPosition'] = __flagship_stations[stationData.call_sign].sortPosition;

            // Backwards Compatible Data.
            stationData['callLetters'] = stationData.call_sign;
            stationData['commonName'] = stationData.full_common_name;
            stationData['kidsSite'] = stationData.station_kids_url || stationData.website_url;

            // Better mapping for station logo urls.
            for (var i = 0; i < stationData.images.length; i++) {
              var profileName = stationData.images[i].profile;
              stationData[profileName] = stationData.images[i].url;
            }

            return stationData;
          });

          // Sort stations by sortPosition.
          _localization.stations.sort(function(a,b){
            return a.sortPosition - b.sortPosition;
          });

          console.log('Stations with metadata:', {'_localization.stations': _localization.stations});

          _localization.LocalizationEvent.dispatchEvent({
            eventType: _localization.LocalizationEvent.STATION_LIST_CHANGE,
            stations: _localization.stations
          });

          if (_autoLocalize === true && _localization.stations[0]) {
            _localization.updateStation(_localization.stations[0].callLetters, true);
            _autoLocalize = false;
          }
        }
      });
    }

    function onStationLoaded(response, autoLocalized, userInitiated) {
      if (response.data.length == 0 || !response.data[0].attributes) {
        return;
      }

      _localization.station = response.data[0].attributes;

      for (var i = 0; i < _localization.station.images.length; i++) {
        var profileName = _localization.station.images[i].profile;
        _localization.station[profileName] = _localization.station.images[i].url;
      }

      var __backwardsCompatibleData = {
        callLetters: _localization.station.call_sign,
        commonName: _localization.station.full_common_name,
        kidsSite:
          _localization.station.station_kids_url ||
          _localization.station.website_url,
        autoLocalized: Boolean(autoLocalized === true),


        // =======================================
        // The following urls should be removed in
        // version 2.0 of this localization util.
        // =======================================

        //Default Image
        logoURL:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/standard/" +
          _localization.station.call_sign +
          ".gif",

        //PBS GA currated images
        // 2.29:1 (78 x 34 px)
        main:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/main/" +
          _localization.station.call_sign +
          ".png",
        viralplayer:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/viralplayer/" +
          _localization.station.call_sign +
          ".png",

        // 2.79:1 (78 x 28 px)
        smallbw:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/smallbw/" +
          _localization.station.call_sign +
          ".gif",

        // 1:1 (75 x 75 px)
        apps:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/apps/" +
          _localization.station.call_sign +
          ".png",
        findersml:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/findersml/" +
          _localization.station.call_sign +
          ".gif",
        donate:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/station-logos/donate-button/" +
          _localization.station.call_sign +
          ".gif",
        pbsmain:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/station-logos/pbs.org/" +
          _localization.station.call_sign +
          ".gif",

        //PBS KIDS currated images
        // 57 x 47px
        standard:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/standard/" +
          _localization.station.call_sign +
          ".gif",

        // 150 x 77px
        ipadLogoURL:
          "https://web.archive.org/web/20251021154112/https://www-tc.pbs.org/images/stations/ipad/" +
          _localization.station.call_sign +
          ".png"
      };

      // Backfill backwards compatible data.
      for (var j in __backwardsCompatibleData) {
        _localization.station[j] = __backwardsCompatibleData[j];
      }

      _setCookie(
        "pbskids.station",
        _localization.station.call_sign,
        2 * 365,
        "/",
        ".pbskids.org"
      );
      _setCookie(
        "pbskids.autolocalized",
        Boolean(autoLocalized === true),
        2 * 365,
        "/",
        ".pbskids.org"
      );

      $("body").addClass("localized");
      $("body").toggleClass("autolocalized", autoLocalized === true);
      setProducerTVTimesLink(_localization.station);

      _localization.localized = true;
      _localization.autoLocalized = autoLocalized;
      _localization.LocalizationEvent.dispatchEvent({
        eventType: _localization.LocalizationEvent.STATION_CHANGE,
        station: _localization.station
      });

      if (userInitiated === true && window.GA_obj && window.GA_obj.trackEvent) {
        window.GA_obj.trackEvent(
          "Links",
          "Station Localization",
          _localization.station.call_sign
        );
      }

      _log("Localized: ", _localization);
    }

    /* Update HTML Methods
    **************************/
    function onZipChange(e) {
      $(".pbskids-station-picker form.pbskids-get-zipcode .input-zipcode").val(
        e.zipcode
      );
      $(".pbskids-station-picker form.pbskids-get-zipcode").hide();
      $(".pbskids-station-picker footer .current-zipcode").html(e.zipcode);
      $(".pbskids-station-picker article").css("display", "");
    }

    function onStationListChange(e) {
      $(".pbskids-station-picker ul.pbskids-station-list li").off();
      $(".pbskids-station-picker ul.pbskids-station-list").empty();

      _log('e.stations', e.stations);
      var __lim = Math.min(5, e.stations.length);
      for (var i = 0; i < __lim; i++) {
        $(".pbskids-station-picker ul.pbskids-station-list").append(
          "<li data-update-station='" + e.stations[i].callLetters + "'>" +
            "<img src='" +
            (e.stations[i]['color-single-brand-logo'] || e.stations[i]['color-cobranded-logo']) +
            "' alt='" +
            e.stations[i].callLetters +
            " station logo' />" +
            e.stations[i].commonName +
            "</li>"
        );
      }
      _localization.attachStationClickHandlers();
    }

    function setProducerTVTimesLink(station) {

      /** If a TV times link is on the page, update its value and unhide it.
       * Usage: Producer adds data-pbs-kids-tvss-link and style="display: none"
       * attributes to either a link element or its parent. The href will
       * update whenever the station is updated.
      */
      var scheduleUrl = station && (station.tvss_url || station.kidsSite || station.website_url);
      if(scheduleUrl) {
        var tvTimesEl = $('[data-pbs-kids-tvss-link]');
        if(tvTimesEl.is( "a" )) {
          tvTimesEl.attr('href', scheduleUrl).css('display', '');
        } else {
          tvTimesEl.css('display', '').find('a').attr('href', scheduleUrl);
        }
      }
    }

    /* Public Methods
    **************************/
    _localization.updateZip = function(zip_code) {
      /**
      * @zip_code (Optional): (Int) or (String) of the updated zipcode
      * returns the current zip code or "(none)"
      */
      if (zip_code === "fromPicker") {
        return _localization.updateZip(
          $(".pbskids-station-picker .pbskids-get-zipcode .input-zipcode").val()
        );
      }

      if (zip_code) {
        zip_code = zip_code + "";
        if (!zip_code.match(/^[0-9]{5}$/)) {
          return "(not a valid zipcode)";
        }
        updateZip(zip_code);
      }
      return zip_code;
    };

    _localization.showZipCodePicker = function() {
      $(".pbskids-station-picker .pbskids-get-zipcode").css("display", "");
      $(".pbskids-station-picker article").css("display", "none");
    };

    _localization.updateStation = function(
      station_call_letters,
      autoLocalized,
      userInitiated
    ) {
      /**
      * @station_call_letters (Optional): the call-letters of the station to update to, e.g. WETA and WNET.
      * returns Boolean, true or false if the call to fetchStation is made.
      */
      if (
        typeof station_call_letters == "string" &&
        station_call_letters.length == 4
      ) {
        $.ajax({
          url: _STATION_SERVICES,
          dataType: "json",
          data: {
            call_sign: station_call_letters
          },
          success: function(response) {
            onStationLoaded(response, autoLocalized, userInitiated);
          }
        });
        return true;
      }
      return false;
    };

    function attachClickHandler(selector, handler) {
        document.querySelectorAll(selector).forEach(function(ele) {
            if (!ele.getAttribute('data-click-handler-attached')) {
                ele.addEventListener('click', handler, false);
                ele.setAttribute('data-click-handler-attached', true);
            }
        });
    }

    _localization.attachStationClickHandlers = function() {
        attachClickHandler('[data-update-station]', function() {
            _localization.updateStation(
                this.getAttribute('data-update-station')
            );
        });
        attachClickHandler('[data-update-station-manual]', function() {
            _localization.updateStation(
                this.getAttribute('data-update-station-manual'),
                false,
                true
            );
        });
        attachClickHandler('[data-show-zipcode-picker]', function() {
            _localization.showZipCodePicker();
        });
    };

    _localization.getStationPickerHTML = function(containerTagType) {
      containerTagType = containerTagType || "aside";
      var __stationPickerHTML =
        "<" +
        containerTagType +
        ' style="position:relative;" class="pbskids-station-picker"><article class="pbskids-station-list-container" style="' +
        (!_localization.zip ? " display:none;" : "") +
        '"><header><h1>Select your local station</h1></header><p><ul class="pbskids-station-list">';

      if (_localization.stations) {
        _log('_localization.stations', _localization.stations);
        var __lim = Math.min(5, _localization.stations.length);
        for (var i = 0; i < __lim; i++) {
          __stationPickerHTML +=
            "<li data-update-station-manual='" + _localization.stations[i].callLetters + "'><img src='" +
            (_localization.stations[i]['color-single-brand-logo'] || _localization.stations[i]['color-cobranded-logo']) +
            "' alt='" +
            _localization.stations[i].callLetters +
            " station logo'/>" +
            _localization.stations[i].commonName +
            "</li>";
        }
      }

      __stationPickerHTML +=
        '</ul></p><footer>Results for <span class="current-zipcode">' +
        (_localization.zip || "") +
        '</span>. <a class="change-zipcode" data-show-zipcode-picker>Try another zip code.</a></footer></article><form name="pbskids-get-zipcode" class="pbskids-get-zipcode" action="javascript:void(0);" onsubmit="org.pbskids.localization.updateZip(\'fromPicker\');" style="background:#FFF; text-align:center; padding:20px 0; ' +
        (_localization.zip ? " display:none;" : "") +
        '"><label for="station-picker-zipcode-input" style="display: block;">What is your zip code?</label><span style="display:block">PBS KIDS uses your zip code to find our stations in your area.</span><input id="station-picker-zipcode-input" name="zipcode" class="input-zipcode" type="text" maxlength="5" placeholder="zip code" value="' +
        (_localization.zip || "") +
        '" style="text-align:center;"/><input type="submit" value="Go"/></form></' +
        containerTagType +
        ">";

      return __stationPickerHTML;
    };

    _localization.StationPicker = function(stationFieldID) {
      _log("StationPicker");

      var __openStationFinder = function(e) {
        _log("__openStationFinder()");
        $("#pbskids-station-picker").addClass("show-station-finder");
      };

      var __closeStationFinder = function(e) {
        _log("__closeStationFinder()");
        $("#pbskids-station-picker").removeClass("show-station-finder");
        return false;
      };

      var __onStationSelected = function(e) {
        _log("__onStationSelected()");
        $("#" + stationFieldID).val(e.station.callLetters);
        $("#pbskids-station-picker .current-station-logo").html(
          '<img src="' +
            e.station['color-single-brand-logo'] || e.station['color-cobranded-logo'] +
            '" alt="' +
            e.station.callLetters +
            ' station logo" />' +
            e.station.commonName
        );
        $("#pbskids-station-picker .find-station-button").html(
          "Not your station? Select another."
        );
        __closeStationFinder();
      };

      // Configure station input field
      $("#" + stationFieldID)
        .prop("type", "hidden")
        .val(_localization.station ? _localization.station.callLetters : "")
        .parent()
        .append(
          '<aside id="pbskids-station-picker" >' +
            '<p class="station-group">' +
            '<span class="current-station-logo">' +
            (_localization.station
              ? '<img src="' +
                _localization.station['color-single-brand-logo'] || _localization.station['color-cobranded-logo'] +
                '" alt="' +
                _localization.station.callLetters +
                ' station logo"/>' +
                _localization.station.commonName
              : "") +
            "</span>" +
            '<a class="find-station-button">' +
            (_localization.station
              ? "Not your station? Select another."
              : "Find your local station") +
            "</a>" +
            "</p>" +
            _localization.getStationPickerHTML(/*"article"*/) +
            '<button class="exit-station-finder">Back</button>' +
            "</aside>"
        );
        _localization.attachStationClickHandlers();

      // Add css
      $("head").append(
        '<link rel="stylesheet" type="text/css" href="' +
          _headband_root + 'sass/station-picker.css">'
      );

      // Add event-listeners
      $(document).on(
        _localization.LocalizationEvent.STATION_CHANGE,
        __onStationSelected
      );
      $("#pbskids-station-picker .exit-station-finder").click(
        __closeStationFinder
      );
      $("#pbskids-station-picker .find-station-button").click(
        __openStationFinder
      );
    };

    //Complete and return the Global Localization Object, (window|exports).org.pbskids.localization
    init();
    return _localization;
  });
})();

}

/*
     FILE ARCHIVED ON 15:41:12 Oct 21, 2025 AND RETRIEVED FROM THE
     INTERNET ARCHIVE ON 00:02:05 Feb 03, 2026.
     JAVASCRIPT APPENDED BY WAYBACK MACHINE, COPYRIGHT INTERNET ARCHIVE.

     ALL OTHER CONTENT MAY ALSO BE PROTECTED BY COPYRIGHT (17 U.S.C.
     SECTION 108(a)(3)).
*/
/*
playback timings (ms):
  captures_list: 0.775
  exclusion.robots: 0.022
  exclusion.robots.policy: 0.009
  esindex: 0.012
  cdx.remote: 25.87
  LoadShardBlock: 366.642 (6)
  PetaboxLoader3.datanode: 550.228 (7)
  load_resource: 330.757
  PetaboxLoader3.resolve: 98.953
*/