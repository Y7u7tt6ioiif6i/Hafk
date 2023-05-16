<!doctype html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta name="description" content="">
  <meta name="authors" content="Bo Zhao, Fengyu Xu, Le Kang, Joshua Ji, Steven Bao, and Jou Ho">
  <!-- <meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
  <meta http-equiv="Pragma" content="no-cache" />
  <meta http-equiv="Expires" content="0" /> -->
  <title>Novel Coronavirus Infection Map</title>
  <link rel="stylesheet" href="css/bootstrap.min.css">
  <link rel="stylesheet" href="css/leaflet.css" />
  <link rel="stylesheet" href="css/MarkerCluster.Default.css">
  <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css">
  <link href="https://fonts.googleapis.com/css?family=Titillium+Web|Oswald" rel="stylesheet">
  <link href="css/c3.min.css" rel="stylesheet">
  <link rel="stylesheet" href="css/simplebar.css" />
  <link rel="stylesheet" href="css/animate.min.css">
  <link href="css/bootstrap4-toggle.min.css" rel="stylesheet">
  <link rel="stylesheet" href="css/main.css">
  <link rel="stylesheet" href="css/mobile.css">
  <link rel="icon" href="img/favicon.ico" type="image/x-icon">
  <script src="js/d3.js"></script>
  <script src="js/c3.min.js"></script>
  <script src="js/leaflet.js"></script>
  <script src="js/leaflet.markercluster.js"></script>
  <script src="js/leaflet-polygon.fillPattern.js"></script>
  <script src="js/topojson.v1.min.js"></script>
  <script src="js/chroma.min.js"></script>
  <script src="js/jquery-3.3.1.min.js"></script>
  <script type="text/javascript" src="js/jquery.sparkline.min.js"></script>
  <script src="js/bootstrap.min.js"></script>
  <script src="js/bootstrap4-toggle.min.js"></script>
  <script src="js/bootstrap.bundle.min.js"></script>
  <script src="js/simplebar.min.js"></script>
</head>

<body>
  <div class="modal fade" id="overlay">
    <div class="modal-dialog" style="max-width: 60%;">
      <div class="modal-content">
        <div class="modal-header">
          <h3 class="modal-title">Notice</h3>
          <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
        </div>
        <div class="modal-body">
          <p>We have decided to stop updating the website on June 27th, 2021. Thank you very much for following us since the beginning of the COVID-19 pandemic. Our initial goal of creating this platform is to help inform and educate the general
            public on this global public health crisis through using GIS technologies. Since January 2020, more than 1.8 million users have accessed our website. We received many positive comments on our integrative approach of collecting and
            visualizing global COVID-19 case data, especially during the early phase of the pandemic. We sincerely appreciate your recognition of our work and all the valuable feedback you provided to us.
            <br>
            <br>
            One and a half years after the start of the pandemic, with the wide adoption of vaccination, it is good to see that the overall situation is getting better and better. Meanwhile, better standards for COVID-19 data collection and
            presentation have been established by public health organizations in all parts of the world. Therefore, we think it is time to stop our service and encourage people to follow the information published by official sources, such as the
            Centers for Disease Control and Prevention and the World Health Organization.
            <br>
            <br>
            Thank you again for your support!
            <br>
            <br>
            <br>
            Stay well,
            <br>
            UW HGIS Lab
          </p>
        </div>
      </div>
    </div>
  </div>
  <main>
    <div class="loader"></div>
    <div id="mobiledeck">
      <p>
        <span class="mobile-title">Aggr. Confirmed</span>
        <span class="confirmed-count"></span>
        <span class="confirmed-new-count "></span>
      <p>

      <p>
        <span class="mobile-title">Active Confirmed</span>
        <span class="active-count"></span>
        <span class="active-new-count"></span>
      <p>

      <p>
        <span class="mobile-title">Recovered</span>
        <span class="recovered-count"></span>
        <span class="recovered-new-count"></span>
      <p>

      <p>
        <span class="mobile-title">Death</span>
        <span class="death-count"></span>
        <span class="death-new-count"></span>
      <p>
    </div>

    <div id="info" data-simplebar data-simplebar-auto-hide="true">
      <div id="title" style="font-size:19px"><img src="img/virus_logo.png" width="28px"> Novel Coronavirus (COVID-19) Infection Map
        <span><a href="https://twitter.com/UW" target="_blank"><i class="fab fa-twitter-square"></i></a></span>
        <span><a href="https://github.com/jakobzhao/virus" target="_blank"><i class="fab fa-github-square"></i></a></span>
        <span><a data-toggle="modal" data-target="#resourcewindow"><i class="far fa-newspaper"></i></a></span>
        <span><a data-toggle="modal" data-target="#infowindow"><i class="nav fas fa-question-circle"></i></a></span>
      </div>

      <p><span id="placename">GLOBAL TREND</span> </p>
      <div><span id="last-date">Last update: </span><span id="date"></span> <span id="hint"> Click a place to review local trend.</span></div>
      <p><span id="source">Source: </span><span id="source-website" href="" target="_blank"></span></p>
      <div id="deck-1" class="card-deck counts">
        <div class="card">
          <div class="card-body confirmed">
            <h5 class="card-title">Aggregated Confirmed
              <i class="nav fas fa-exclamation-circle tooltip">
                <span class="tooltiptext">All the confirmed cases ever since the discovery of the COVID-19 in the statistical area.</span>
              </i>
            </h5>
          </div>
          <p class="card-text">
            <span class="confirmed-count"></span><span class="confirmed-new-count">
            </span>
          </p>
        </div>
        <div class="card">
          <div class="card-body death">
            <h5 class="card-title">Death</h5>
            <p class="card-text"><span class="death-count"></span><span class="death-new-count"></span></p>
          </div>
        </div>
      </div>
      <div id="deck-2" class="card-deck counts">
        <div class="card">
          <div class="card-body active">
            <h5 class="card-title">Active Confirmed
              <i class="nav fas fa-exclamation-circle tooltip">
                <span class="tooltiptext">The remaining confirmed cases. The active confirmed cases excludes the recovered and death cases.</span>
              </i>
            </h5>
          </div>
          <p class="card-text">
            <span class="active-count"></span>
            <span class="active-new-count"></span>
            <i id="counticon" class="nav fas fa-exclamation-circle tooltip counticon active-new-count-tooltip">
              <span class="tooltiptext">The newly increased/decreased confirmed cases: the # of today's active confirmed cases subtract the # of yesterday's.</span>
            </i>
          </p>
        </div>
        <div class="card">
          <div class="card-body recovered">
            <h5 class="card-title">Recovered</h5>
            <p class="card-text"><span class="recovered-count"></span><span class="recovered-new-count"></span></p>
          </div>
        </div>
      </div>

      <div class="dropdown">
        <button class="btn btn-secondary btn-sm dropdown-toggle" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          linear option
        </button>
        <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
          <a class="dropdown-item" id="linear">linear</a>
          <a class="dropdown-item" id="logarithm">logarithm</a>
        </div>
      </div>

      <p class="chart-legend"> toggle on/off the curve or scroll on the curves to change the date range </P>

      <div id="timeline-chart"></div>
      <div id="total-chart"></div>
      <div id="rank-chart"></div>

      <div id="footer">
        <div id="mtToggle">
          <span id="rankingText"> <b> World or U.S. Rankings</b> </span>
          <!-- #e8e3d3; -->
          <!-- #dc3545; -->
          <span id="rankingIcon"><i style="margin-left:10px;color:#dc3545" class="fas fa-angle-double-right animated infinite slideInLeft delay-2s" style="gray"></i></span>
          <span id="rankingSpace" style="margin-right:1px"> </span>
          <input type="checkbox" id="panelSwitcher" unchecked data-toggle="toggle" data-off="Situational Heatmap" data-width="180" data-size="xs" data-on="Back to Map" data-onstyle="secondary" data-offstyle="outline-secondary">
          <span style="margin-right:25px"> </span>
          <span id="rankingToggle"><input type="checkbox" id="areaSwitcher" unchecked data-toggle="toggle" data-on="Global Rank" data-width="100" data-size="xs" data-off="U.S. Rank" data-onstyle="secondary" data-offstyle="outline-secondary">
          </span>
        </div>

        <div id="content-explain"> In the main map, an country or region's inflection level is measured by the # of today's active/remaining confirmed cases. The gray slash texture indicates no previous cases are discovered;
          the green
          texture means the region in which all the infected cases have recovered.</div>

        <div><i class='fas fa-users' style="color:#dc3545"></i> &nbsp; Infection Case(s) indicates one or several confirmed infected individual(s) in the U.S., excluding those were identified from the Diamond Princess.
          The dataset of the infected cases are continuously enriched from different data portals such as
          <a href="https://coronavirus.1point3acres.com/en" target="_blank">1point3acres</a> and state officials. Notably, <span class="emphasis"> each case was geocoded to an
            approximate location within the county
            which reported the case. The location is by no means identical to the exact address where the case was discovered.</span>
        </div>

        <!--
        <div> <i class="fas fa-procedures" style="color:#dc3545"> </i> &nbsp; An Infected Community indicates a community or village where confirmed cases were found. The local governments in China have taken strict measures to isolate the residents
          of
          these
          places from the outside. The dataset of infected community can be found at <a href="https://lab.ahusmart.com/nCoV/api/detail" target="_blank">ahusmart</a>.
        </div>
      -->

        <div>This map is made by the <a href="http://hgis.uw.edu" target="_blank">Humanistic GIS Lab at University of Washington - Seattle</a>.
          The data are mainly collected from <a href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/" target="_blank">WHO</a>,
          <a href="https://www.cdc.gov/coronavirus/2019-ncov/cases-in-us.html" target="_blank">CDC</a>,
          <a href="https://www.canada.ca/en/public-health/services/diseases/2019-novel-coronavirus-infection.html" target="_blank">PHA</a> ,
          <a href="http://2019ncov.chinacdc.cn/2019-nCoV/" target="_blank">China CDC</a>,
          <a href="https://www.nbcnews.com/health/health-news/coronavirus-u-s-map-where-virus-has-been-confirmed-across-n1124546" target="_blank">NBC News</a>,
          <a href="https://en.wikipedia.org/wiki/Template:2019%E2%80%9320_coronavirus_pandemic_data" target="_blank">Wikipedia</a>, <a target="_blank" href="https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html">New York Times</a>,
          and <a href="https://voice.baidu.com/act/newpneumonia/newpneumonia" target="_blank">Baidu</a>. Regarding the state level data in the U.S., they are collected from CDC, state officials, <a target="_blank"
            href="https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html">New York Times</a>, and <a href="https://www.nbcnews.com/health/health-news/coronavirus-u-s-map-where-virus-has-been-confirmed-across-n1124546"
            target="_blank">NBC News</a>.
          The computational resources are provided by <a href="https://csde.washington.edu/" target="_blank">UW's Center for Studies in Demography and Ecology</a>. The base maps are from <a target="_blank"
            href="https://github.com/CartoDB/cartodb/wiki/BaseMaps-available">Carto</a> and <a href="https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/" target="_blank">ESRI</a>, and the geospatial data for the base maps
          are acquired from the <a href="openstreetmap.org/copyright" target="_blank"> OpenStreetMap</a>.
          <span class="emphasis">The timely updated dataset of the virus infection can be downloaded <a href="http://hgis.uw.edu/virus/assets/virus.csv" target="_blank">here.</a></span> Details
          about this interactive
          map can be found <a data-toggle="modal" data-target="#infowindow"> here</a>. If you have any questions or
          concerns, please contact <a href="mailto:zhaobo@uw.edu">Bo Zhao</a>.
        </div>
        <p align="right" style="margin-right:20px; margin-top:-25px"><a href="https://hgis.uw.edu/2020/03/18/covid-19-novel-coronavirus-infection-map/" target="_blank"><img src="img/logo.png" width="120px"></img></a></p>

      </div>

    </div>
    <div id="table">
      <div id="table-container" data-simplebar data-simplebar-auto-hide="true">
        <table id="table-container-div" class="table table-bordered table-fixed table-hover">
          <thead>
          </thead>
          <tbody>
          </tbody>
        </table>
      </div>
    </div>

    <div id="legend-panel" class="card-deck legend">

      <div class="card">
        <div class="card-body">
          <h5 class="card-title grey-circles" style="color:black">no case</h5>
        </div>
      </div>

      <div class="card">
        <div class="card-body legend-color-1">
          <h5 class="card-title" style="color:black">1</h5>

        </div>
      </div>

      <div class="card">
        <div class="card-body legend-color-2">
          <h5 class="card-title" style="color:black">100</h5>

        </div>
      </div>
      <div class="card">
        <div class="card-body  legend-color-3">
          <h5 class="card-title" style="color:black">1,000</h5>
        </div>
      </div>

      <div class="card">
        <div class="card-body  legend-color-4">
          <h5 class="card-title" style="color:black">5,000</h5>

        </div>
      </div>

      <div class="card">
        <div class="card-body legend-color-5">
          <h5 class="card-title" style="color:black">10,000</h5>
        </div>
      </div>

      <div class="card">
        <div class="card-body legend-color-6">
          <h5 class="card-title" style="color:black">50,000+</h5>
        </div>
      </div>
    </div>
    <div id="map"></div>

  </main>
  <div id="infowindow" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered" role="document" style="width:1250px!important">
      <div class="modal-content">
        <div class="modal-header">
          <strong class="modal-title" id="exampleModalLongTitle">Info</strong>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div id="demo" class="carousel " data-ride="carousel">
            <p>This online interactive map enables users to track both the global and local trends of Novel Coronavirus infection since Jan 21st, 2020. The supporting dataset is timely collected from multiple official sources and then plotted onto
              this map.</p>
            <h5>Data Sources</h5>
            <p>The data are mainly collected from 1. <a href="http://www.nhc.gov.cn" target="_blank">National Health Commission</a> (NHC) of the People’s Republic of China
              2. China’s Provincial & Municipal Health Commission, China’s Provincial & Municipal government database
              3. Public data published from Hongkong, Macau, and Taiwan official channels
              4. <a href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/" target="_blank">World Health Organization</a> (WHO)
              5. <a href="https://www.cdc.gov/coronavirus/2019-ncov/cases-in-us.html" target="_blank">Centers for Disease Control and Prevention</a> (CDC)
              6. <a href="https://www.canada.ca/en/public-health/services/diseases/2019-novel-coronavirus-infection.html" target="_blank">Public Health Agency of Canada</a> (PHAC)
              7. <a href="https://voice.baidu.com/act/newpneumonia/newpneumonia" target="_blank">Baidu</a>.
              <!--
              8. <a href="https://lab.ahusmart.com/nCoV/api/detail" target="_blank">ahusmart</a> - the infected community in China.
              -->
              8. the state officals of different states in the U.S.
              9. <a href="https://www.nbcnews.com/health/health-news/coronavirus-u-s-map-where-virus-has-been-confirmed-across-n1124546" target="_blank">NBC News</a>.
              10. <a target="_blank" href="https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html">New York Times</a>

              The dataset (in SQLite format) can be downloaded from <a href="http://hgis.uw.edu/virus/assets/virus.db" target="_blank">here</a>.
              You can view the data (in CSV format) at <a href="http://hgis.uw.edu/virus/assets/virus.csv" target="_blank">here</a>.
            </p>

            <p>In the data table, each entry indicates the infection status in the format of "#-#-#-#" -- a 4-sequel entry divided by dashes. The first sequel represents the number of confirmed cases, the second sequel represents suspected
              cases, the third sequel represents cured cases, the fourth sequel represents death cases.</p>

            <h5>Update Procedure</h5>

            <p>The country-level data is collected from WHO, while the data of each province in China is collected from multiple sources such as China's NHC，Mapmiao and Baidu. Notably, we also refer to CDC to verify the virus spreading status in the
              U.S. To
              make a timely data and map updates, we collect the data every 4 hours, and verify the data quality per day. In addition, we plan to provide finer-scale data from China (the county level), U.S. (the state level) and Canada (the province
              level) in the next version.</p>

            <h5>Acknowledgment</h5>
            <p>
              <li>Team members: Bo Zhao, Fengyu Xu, Le Kang, Joshua Ji, Steven Bao, and Jou Ho.</li>
              <li>The Server is hosted at UW’s <a href="https://https://csde.washington.edu/" target="_blank">Center for Studies in Demography and Ecology (CSDE)</a>.</li>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div id="resourcewindow" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered" role="document" style="width:1250px!important">
      <div class="modal-content">
        <div class="modal-header">
          <strong class="modal-title" id="exampleModalLongTitle">Resource</strong>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div id="demo" class="carousel " data-ride="carousel">
            <h5>Coronavirus information resources</h5>
            <!-- <br><b> China - Official Websites</b> -->
            <table style="width:100%">
              <tr>
                <td><a href="http://wjw.beijing.gov.cn/xwzx_20031/wnxw/" target="_blank"> Beijing</a></td>
                <td><a href="http://wsjkw.hebei.gov.cn/list/more_newlist_14.html" target="_blank"> Hebei</a></td>
                <td><a href="http://wsjk.ln.gov.cn/wst_zdzt/xxgzbd/yqtb/" target="_blank"> Liaoning</a></td>
                <td><a href=" http://www.jl.gov.cn/szfzt/jlzxd/yqtb/" target="_blank"> Jilin</a></td>
              </tr>
              <tr>
                <td><a href="http://wjw.jiangsu.gov.cn/col/col7290/index.html" target="_blank"> Jiangsu</a></td>
                <td><a href="http://wsjkw.sh.gov.cn/yqfk2020/" target="_blank"> Shanghai</a></td>
                <td><a href="http://hc.jiangxi.gov.cn/ztxx/xxgzbdgrdfyyqfk/yqtb/index.shtml" target="_blank"> Jiangxi</a></td>
                <td><a href="http://wsjkw.gd.gov.cn/zwyw_yqxx/" target="_blank"> Guangdong</a></td>
              </tr>
              <tr>
                <td><a href="http://wjw.hunan.gov.cn/wjw/qwfb/yqfkgz_list.html" target="_blank"> Hunan</a></td>
                <td><a href="http://wst.hainan.gov.cn/yqfk/" target="_blank"> Hainan</a></td>
                <td><a href="https://www.zjwjw.gov.cn/col/col1202112/index.html" target="_blank"> Zhejiang</a></td>
                <td><a href="http://www.hnwsjsw.gov.cn/channels/854.shtml" target="_blank"> Henan</a></td>
              </tr>
              <tr>
                <td><a href="http://hc.jiangxi.gov.cn/ztxx/xxgzbdgrdfyyqfk/yqtb/index.shtml" target="_blank"> Jiangxi</a></td>
                <td><a href="http://wjw.hubei.gov.cn/bmdt/ztzl/fkxxgzbdgrfyyq/xxfb/" target="_blank"> Hubei</a></td>
                <td><a href=" http://sxwjw.shaanxi.gov.cn/col/col9/index.html" target="_blank"> Shaanxi</a></td>
                <td><a href="http://wjw.shanxi.gov.cn/wjywl02/index.hrh" target="_blank"> Shanxi</a></td>
              </tr>
              <tr>
                <td><a href="http://wsjkw.nx.gov.cn/yqfkdt/yqsd1.htm" target="_blank"> Ningxia</a></td>
                <td><a href="https://wsjkw.qinghai.gov.cn/ztbd/yqjk/fkdt/2020/02/18/1582009147575.html" target="_blank"> Qinghai</a></td>
                <td><a href="http://wsjk.gansu.gov.cn/channel/11217/index.html" target="_blank"> Gansu</a></td>
                <td><a href="http://xjhfpc.gov.cn/ztzl/fkxxgzbdfygz/yqtb.htm" target="_blank"> Xinjiang</a></td>
              </tr>
              <tr>
                <td><a href="http://www.gzhfpc.gov.cn/ztzl_500663/xxgzbdgrdfyyqfk/" target="_blank"> Guizhou</a></td>
                <td><a href="http://ynswsjkw.yn.gov.cn/wjwWebsite/web/col?id=UU157976428326282067&cn=xxgzbd&pcn=ztlm&pid=UU145102906505319731" target="_blank"> Yunnan</a></td>
                <td><a href="http://wsjkw.cq.gov.cn/topic/25.jspx" target="_blank"> Chongqing</a></td>
                <td><a href="http://wjw.xizang.gov.cn/xwzx/wsjkdt/" target="_blank"> Xizang</a></td>
              </tr>
              <tr>
                <td><a href="http://wjw.nmg.gov.cn/xwzx/xwfb/index.shtml" target="_blank"> Neimenggu</a></td>
                <td><a href="http://wsjkw.sc.gov.cn/scwsjkw/gzbd01/ztwzlmgl.shtml" target="_blank"> Sichuan</a></td>
                <td><a href="http://wsjkw.hlj.gov.cn/index.php/Home/Zwgk/all/typeid/42" target="_blank"> Heilongjiang</a></td>
                <td><a href="https://v.gxnews.com.cn/zt/2020yq" target="_blank"> Guangxi</a></td>
              </tr>
              <tr>
                <td><a href="http://wjw.ah.gov.cn/news_list_477_1.html" target="_blank"> Anhui</a></td>

                <td><a href="https://www.ssm.gov.mo/apps1/PreventWuhanInfection/ch.aspx#clg17046" target="_blank"> Macau</a></td>
                <td><a href="https://sites.google.com/cdc.gov.tw/2019ncov/taiwan" target="_blank"> Taiwan</a></td>
                <td><a href="https://www.chp.gov.hk/files/pdf/enhanced_sur_pneumonia_wuhan_chi.pdf" target="_blank"> Hongkong</a></td>
              </tr>
              <!-- </table>
            <br><b> the US - Official Websites</b>
            <table style="width:100%"> -->
              <tr>
                <td><a href="http://www.alabamapublichealth.gov/infectiousdiseases/2019-coronavirus.html" target="_blank">Alabama</a></td>
                <td><a href="https://dphhs.mt.gov/publichealth/cdepi/diseases/coronavirusmt" target="_blank">Montana</a></td>
                <td><a href="http://dhss.alaska.gov/dph/Epi/id/Pages/COVID-19/monitoring.aspx" target="_blank">Alaska</a></td>
                <td><a href="http://dhhs.ne.gov/Pages/Coronavirus.aspx" target="_blank">Nebraska</a></td>
              </tr>
              <tr>
                <td><a href="https://www.azdhs.gov/preparedness/epidemiology-disease-control/infectious-disease-epidemiology/index.php#novel-coronavirus-home" target="_blank">Arizona</a></td>
                <td><a href="http://dpbh.nv.gov/Programs/OPHIE/dta/Hot_Topics/Coronavirus/" target="_blank">Nevada</a></td>
                <td><a href="https://www.healthy.arkansas.gov/programs-services/topics/novel-coronavirus" target="_blank">Arkansas</a></td>
                <td><a href="https://www.dhhs.nh.gov/dphs/cdcs/2019-ncov.htm" target="_blank">New Hampshire</a></td>
              </tr>
              <tr>
                <td><a href="https://www.cdph.ca.gov/Programs/CID/DCDC/Pages/Immunization/ncov2019.aspx" target="_blank">California</a></td>
                <td><a href=" https://www.colorado.gov/pacific/cdphe/2019-novel-coronavirus" target="_blank">Colorado</a></td>
                <td><a href="https://cv.nmhealth.org/" target="_blank">New Mexico</a></td>
                <td><a href=" https://portal.ct.gov/coronavirus" target="_blank">Connecticut</a></td>
              </tr>
              <tr>
                <td><a href=" https://health.ny.gov/diseases/communicable/coronavirus/" target="_blank">New York</a></td>
                <td><a href="https://www.dhss.delaware.gov/dhss/dph/epi/2019novelcoronavirus.html" target="_blank">Delaware</a></td>
                <td><a href="https://coronavirus.dc.gov/page/coronavirus-surveillance-data" target="_blank">The District of Columbia</a></td>
                <td><a href="https://www.health.nd.gov/diseases-conditions/coronavirus/north-dakota-coronavirus-cases" target="_blank">North Dakota</a></td>
              </tr>
              <tr>
                <td><a href="http://www.floridahealth.gov/diseases-and-conditions/COVID-19/index.html" target="_blank">Florida</a></td>
                <td><a href="https://coronavirus.ohio.gov/wps/portal/gov/covid-19/" target="_blank">Ohio</a></td>
                <td><a href="https://dph.georgia.gov/" target="_blank">Georgia</a></td>
                <td><a href="https://www.ok.gov/health/Prevention_and_Preparedness/Acute_Disease_Service/Disease_Information/Coronavirus_Disease_2019/Oklahoma_Response_to_Coronavirus_Disease_2019/index.html" target="_blank">Oklahoma</a></td>
              </tr>
              <tr>
                <td><a href="https://www.oregon.gov/oha/PH/DISEASESCONDITIONS/DISEASESAZ/Pages/emerging-respiratory-infections.aspx" target="_blank">Oregon</a></td>
                <td><a href="https://health.hawaii.gov/docd/advisories/novel-coronavirus-2019/#situation" target="_blank">Hawaii</a></td>
                <td><a href="https://coronavirus.idaho.gov/" target="_blank">Idaho</a></td>
                <td><a href="https://www.health.pa.gov/topics/disease/Pages/Coronavirus.aspx" target="_blank">Pennsylvania</a></td>
              </tr>
              <tr>
                <td><a href="http://dph.illinois.gov/topics-services/diseases-and-conditions/diseases-a-z-list/coronavirus" target="_blank">Illinois</a></td>
                <td><a href="https://www.scdhec.gov/index.php/health/infectious-diseases/viruses/coronavirus-disease-2019-covid-19" target="_blank">South Carolina</a></td>
                <td><a href="https://idph.iowa.gov/Emerging-Health-Issues/Novel-Coronavirus" target="_blank">Iowa</a></td>
                <td><a href="https://doh.sd.gov/news/Coronavirus.aspx" target="_blank">South Dakota</a></td>
              </tr>
              <tr>
                <td><a href="https://chfs.ky.gov/agencies/dph/pages/covid19.aspx" target="_blank">Kentucky</a></td>
                <td><a href="https://www.dshs.state.tx.us/coronavirus/#casecounts" target="_blank">Texas</a></td>
                <td><a href="https://coronavirus.utah.gov/coronavirus-latest-information/" target="_blank">Utah</a></td>
                <td><a href="https://www.maine.gov/dhhs/mecdc/infectious-disease/epi/airborne/coronavirus.shtml" target="_blank">Maine</a></td>
              </tr>
              <tr>
                <td><a href="https://www.healthvermont.gov/response/infectious-disease/2019-novel-coronavirus" target="_blank">Vermont</a></td>
                <td><a href="https://phpa.health.maryland.gov/Pages/Novel-coronavirus.aspx" target="_blank">Maryland</a></td>
                <td><a href="http://www.vdh.virginia.gov/surveillance-and-investigation/novel-coronavirus/" target="_blank">Virginia</a></td>
                <td><a href="https://www.mass.gov/info-details/covid-19-cases-quarantine-and-monitoring" target="_blank">Massachusetts</a></td>
              </tr>
              <tr>
                <td><a href="https://www.doh.wa.gov/Emergencies/Coronavirus" target="_blank">Washington</a></td>
                <td><a href="https://www.michigan.gov/coronavirus" target="_blank">Michigan</a></td>
                <td><a href=" https://dhhr.wv.gov/Coronavirus%20Disease-COVID-19/Pages/default.aspx" target="_blank">West Virginia</a></td>
                <td><a href="https://www.health.state.mn.us/diseases/coronavirus/situation.html" target="_blank">Minnesota</a></td>
              </tr>
              <tr>
                <td><a href="https://www.dhs.wisconsin.gov/outbreaks/index.htm" target="_blank">Wisconsin</a></td>
                <td><a href=" https://msdh.ms.gov/msdhsite/_static/14,0,420.html" target="_blank">Mississippi</a></td>
                <td><a href="https://health.wyo.gov/publichealth/infectious-disease-epidemiology-unit/disease/novel-coronavirus/" target="_blank">Wyoming</a></td>
                <td><a href="https://health.mo.gov/living/healthcondiseases/communicable/novel-coronavirus/" target="_blank">Missouri</a></td>
              </tr>
            </table>
            <br><b>Other Official Websites</b>
            <table style="width:100%">
              <tr>
                <td><a href="https://www.cdc.gov/coronavirus/2019-ncov/cases-in-us.html" target="_blank"> the U.S.</a></td>
                <td><a href=" https://www.canada.ca/en/public-health/services/diseases/2019-novel-coronavirus-infection.html" target="_blank"> Canada</a></td>
                <td><a href="https://www.cdc.go.kr/board/board.es?mid=a20501000000&bid=0015" target="_blank"> Republic of Korean</a></td>
              </tr>
              <tr>
                <td><a href="https://www.mhlw.go.jp/stf/newpage_09571.html" target="_blank"> Japan</a></td>
                <td><a href="https://www.health.gov.au/news/health-alerts/novel-coronavirus-2019-ncov-health-alert#current-status" target="_blank"> Australia</a></td>
                <td><a href="https://www.moh.gov.sg/covid-19" target="_blank"> Singapore</a></td>
              </tr>
              <tr>
                <td><a href="http://www.salute.gov.it/nuovocoronavirus" target="_blank"> Italy</a></td>
                <td><a href="https://www.gov.uk/guidance/coronavirus-covid-19-information-for-the-public" target="_blank"> the UK</a></td>
                <td><a href="http://irangov.ir/cat/509" target="_blank"> Iran</a></td>
              </tr>
            </table>
            <br><b>Other Resources:</b>
            <ul>
              <li><a href="https://www.cdc.gov/coronavirus/2019-ncov/symptoms-testing/testing.html" target="_blank"> CDC-selfchecker</a></li> (coronavirus self-test tool)
              <li><a href="https://covid19.healthdata.org/projections" target="_blank"> Coronavirus Data</a></li> (The cisualization shows the data of coronavirus for all 50 states, so that cities and states can best prepare)
              <li><a href="https://ncov.dxy.cn/" target="_blank"> Dingxiangyuan</a></li> (Update national daily data and educate Coronavirus knowledge)
              <li><a href="http://zhongxinzhiyuan.cn/yiqing_real_time_map.html" target="_blank"> Zhongxinzhiyuan</a></li> (Update the latest news and data visualization)
              <li><a href="http://2019ncov.nosugartech.com/search.html" target="_blank"> Tongchengchaxun</a></li> (Coronavirus confirmed patients' trips query tool)
              <li><a href="https://voice.baidu.com/act/newpneumonia/newpneumonia" target="_blank"> Baidu Coronavirus Data Report</a></li> (Update Global daily data and hot topics about Coronavirus)
              <li><a href="https://www.nejm.org/coronavirus" target="_blank"> The New England Journal of Medicine</a></li> (A collection of articles and other resources on the Coronavirus (Covid-19) outbreak, including clinical reports, management
              guidelines, and commentary)
              <li><a href="http://www.nhc.gov.cn/xcs/pfzs/list_gzbd.shtml" target="_blank"> National Health Commission of the People's Republic of China </a></li> (Coronavirus(Covid-19) legal knowledge)
            </ul>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- <script src="js/main.js"></script> -->
  <script>
    ///////////////////////////////accessary//////////////////////////////////
    $(window).ready(function() {
      $('.loader').fadeOut("slow");
      $('#overlay').modal('show');
    });
    var d3locale = d3.formatDefaultLocale({
      "thousands": ",",
      "grouping": [3],
    });
    L.TopoJSON = L.GeoJSON.extend({
      addData: function(jsonData) {
        if (jsonData.type === 'Topology') {
          for (key in jsonData.objects) {
            geojson = topojson.feature(jsonData, jsonData.objects[key]);
            L.GeoJSON.prototype.addData.call(this, geojson);
          }
        } else {
          L.GeoJSON.prototype.addData.call(this, jsonData);
        }
      }
    });
    // Copyright (c) 2013 Ryan Clark
    // var createLabelIcon = function(labelClass, labelText) {
    //   return L.divIcon({
    //     className: labelClass,
    //     html: labelText
    //   })
    // }
    //
    var worldBounds = L.latLngBounds(
      L.latLng(-60, -100), //Southwest
      L.latLng(80, 15) //Northeast
    );
    //return the totalConfirmed number of given country
    function tc(country) {
      if (country == undefined) {
        country = 0
      } else {
        country = +country.split("-")[0];
      }
      return country;
    }
    //return the totalRecovered number of given country
    function tr(country) {
      if (country.split("-")[2] == undefined) {
        country = 0
      } else {
        country = +country.split("-")[2];
      }
      return country;
    }
    //return the totalDeath number of given country
    function td(country) {
      if (country.split("-")[3] == undefined) {
        country = 0
      } else {
        country = +country.split("-")[3];
      }
      return country;
    }
    //////////////////////////////////////////////////////////////////////////
    //create the base map and set the initial view point
    var mymap = L.map('map', {
      center: [38, -120],
      zoomControl: false,
      zoom: 4,
      maxZoom: 10,
      minZoom: 2,
      worldCopyJump: true
    }).fitBounds(worldBounds);
    // .fitWorld()
    new L.Control.Zoom({
      position: 'topright'
    }).addTo(mymap);
    var gray = L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}@2x.png');
    // var dark = L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}@2x.png').addTo(mymap);
    var voyager =
      L.tileLayer('https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}@2x.png').addTo(mymap);
    var satellite =
      L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}');
    var baseLayers = {
      'CARTO Light': gray,
      // 'Dark': dark,
      'CARTO Voyager': voyager,
      'ESRI Satellite': satellite
    }
    var chart, rchart;
    //create colot scale for both region and legend,and insert the "style" into the "head" tag
    var colors = chroma.scale('YlOrRd').mode('lch').colors(6);
    for (i = 0; i < 6; i++) {
      $('head').append($("<style> .region-color-" + (i + 1).toString() + " { color: " + colors[i] + "; font-size: 15px; text-shadow: 0 0 3px #ffffff;} </style>"));
      $('head').append($("<style> .legend-color-" + (i + 1).toString() + " { background: " + colors[i] + "; font-size: 15px; text-shadow: 0 0 3px #ffffff;} </style>"));
    }
    //create communities object that can add community icon to the map through leaflet
    //chinese cases
    var communities = new L.MarkerClusterGroup({
      spiderfyOnMaxZoom: false,
      singleMarkerMode: true,
      // showCoverageOnHover: false,
      // zoomToBoundsOnClick: false,
      iconCreateFunction: function(cluster) {
        return L.divIcon({
          // html: '<i class="fas fa-procedures community community-marker"> <b>' + cluster.getChildCount() + '</b></i>'
          html: '<i class="fas fa-procedures community community-marker"> <b>' + cluster.getChildCount() + '</b></i>'
        });
      }
    });
    //create cases object that can add community icon to the map through leaflet, the size of the icon is based on the number of cases in that area
    // <20 cases return small size icon, >20 & <100 ruturn large size, >100 return 2x size
    //for america and canada cases
    var cases = new L.MarkerClusterGroup({
      spiderfyOnMaxZoom: true,
      singleMarkerMode: true,
      polygonOptions: {
        fillColor: "red",
        color: 'red',
        weight: 0.5,
        opacity: 0.6,
        fillOpacity: 0.2
      },
      showCoverageOnHover: true,
      // zoomToBoundsOnClick: false,
      iconCreateFunction: function(cluster) {
        cnt = cluster.getChildCount()
        if (cnt >= 100) {
          return L.divIcon({
            // html: '<i class="fas fa-users community community-marker"> <b>' + cluster.getChildCount() + '</b></i>'
            html: '<i class="fas fa-users community community-marker fa-2x "> <b>' + "" + '</b></i>'
          });
        } else if (cnt >= 20 && cnt < 100) {
          return L.divIcon({
            // html: '<i class="fas fa-users community community-marker"> <b>' + cluster.getChildCount() + '</b></i>'
            html: '<i class="fas fa-users community community-marker fa-lg "> <b>' + "" + '</b></i>'
          });
        } else {
          return L.divIcon({
            // html: '<i class="fas fa-users community community-marker"> <b>' + cluster.getChildCount() + '</b></i>'
            html: '<i class="fas fa-users community community-marker fa-sm "> <b>' + "" + '</b></i>'
          });
        }
      }
    }).addTo(mymap);
    //load all datasets through d3 and store them in an array
    Promise.all([
      d3.csv('assets/virus.csv'), //datasets[0]
      d3.json("assets/all-topo-15.json"), //datasets[1]
      //d3.csv('assets/communities.csv'), //chinese cases
      d3.csv('assets/timestamp.txt'), //datasets[3]
      d3.csv('assets/cases.csv'), //America cases
      d3.csv('assets/united-states.txt'), //datasets[5]
      d3.csv('assets/canada-city.txt'), //datasets[6]
      d3.csv('assets/old-name.csv'), //datasets[7] chinese provinces
      d3.csv('assets/cases-canada.csv') //datasets[8]
    ]).then(function(datasets) {
      //read the timestamp in timestamp.txt and add it to map
      $("#date").text(datasets[2][0].timestamp.split(".")[0] + " PST");
      //read data from communities.csv and add each case on to the map with given information
      //cases in china
      //datasets[2].forEach(function(d) {
      //  L.marker([parseFloat(d.lat), parseFloat(d.lng)]).bindPopup(d.name + "&nbsp;&nbsp;(<a target='_blank' href='https://translate.google.com/#view=home&op=translate&sl=zh-CN&tl=en&text=" + d.name + "'>Translate to English</a>)").addTo(
      //    communities);
      //})
      //read data from cases.csv and add each case on to the map with given information
      //cases in America
      datasets[3].forEach(function(d) {
        //console.log(d.id)
        L.marker([parseFloat(d.lat), parseFloat(d.lng)]).bindPopup("<b>" + d.no + "</b> <p>" + d.note + " identified on " + d.date + ", &nbsp;<a href='https://" + d.reference + "' target='_blank'>" + d.reference + "</a>.</p>").addTo(
          cases);
      })
      //cases in Canada
      datasets[7].forEach(function(d) {
        //console.log(d.id)
        L.marker([parseFloat(d.lat), parseFloat(d.lng)]).bindPopup("<b>" + d.no + "</b> <p>" + d.note + " identified on " + d.date + ", &nbsp;<a href='https://" + d.reference + "' target='_blank'>" + d.reference + "</a>.</p>").addTo(
          cases);
      })
      var latest = datasets[0][datasets[0].length - 1];
      //delete latest["datetime"];
      //get latest data for every country/city
      var top = {},
        ustop = {},
        cntop = {};
      top["china"] = 0;
      //this fucntion read the latest data from virus.csv and write the country name and it's latest active confirmed value into dictionary
      Object.keys(latest).forEach(function(d) {
        value = tc(datasets[0][datasets[0].length - 1][d]) - tr(datasets[0][datasets[0].length - 1][d]) - td(datasets[0][datasets[0].length - 1][d]);
        // value = tc(datasets[0][datasets[0].length - 1][d]);
        if (datasets[6]["columns"].includes(d)) { //china
          // console.log(value);
          // console.log(top["china"]);
          top["china"] += +value;
          cntop[d] = value;
        } else if (datasets[5]["columns"].includes(d)) { //canada
          ;
        } else if (datasets[4]["columns"].includes(d)) { //us
          ustop[d] = value;
        } else if (d != "datetime") { //else
          top[d] = value;
        }
      })
      // this function take a dictionary [country:active confirmed case], return a dictionary that sorted by the number of active confired case
      function sortJsObject(obj) {
        items = Object.keys(obj).map(function(key) {
          return [key, obj[key]];
        });
        items.sort(function(first, second) {
          return second[1] - first[1];
        });
        sorted_obj = {}
        $.each(items, function(k, v) {
          use_key = v[0]
          use_value = v[1]
          sorted_obj[use_key] = use_value
        })
        return (sorted_obj)
      }
      stop = sortJsObject(top); //sort globally
      sustop = sortJsObject(ustop); //sort US states
      var places = {};
      //this function take a string of country/place name and calculate the data for it
      //return place[name] which is a dictonary that has everyday's dataset
      function calPlace(name) {
        var place = {}
        place[name] = {
          't': ['t'], //date
          'c': ['Aggr. Confirmed'],
          's': ['s'],
          'r': ['Recovered'],
          'd': ['Death'],
          'a': ['Active Confirmed']
        }
        // cf = 0, sp = 0, rc = 0, dd = 0, active = 0;
        datasets[0].forEach(function(d) {
          var USTd = new Date(d["datetime"]);
          place[name].t.push(USTd.setHours(USTd.getHours() + 8)); //convert to American time zone
          cf = 0, sp = 0, rc = 0, dd = 0, active = 0;
          current = d;
          delete current["datetime"];
          if (name == "Global Trend") {
            Object.values(current).forEach(function(d) {
              if (d == undefined) {
                d = "0"
              };
              items = d.split("-");
              switch (items.length) {
                case 4:
                  dd += +items[3];
                case 3:
                  rc += +items[2];
                case 2:
                  sp += +items[1];
                case 1:
                  cf += +items[0];
                  break;
              };
              active = cf - dd - rc;
            });
            cf -= (tc(current["alabama"]) + tc(current["alaska"]) + tc(current["arizona"]) + tc(current["arkansas"]) + tc(current["california"]) + tc(current["colorado"]) + tc(current["connecticut"]) + tc(current["delaware"]) + tc(current[
                "florida"]) + tc(current["georgia usa"]) + tc(current["hawaii"]) + tc(current["idaho"]) + tc(current["illinois"]) + tc(current["indiana"]) + tc(current["iowa"]) + tc(current["kansas"]) + tc(current["kentucky"]) + tc(current[
                "louisiana"]) + tc(current["maine"]) + tc(current["maryland"]) + tc(current["massachusetts"]) + tc(current["michigan"]) + tc(current["minnesota"]) + tc(current["mississippi"]) + tc(current["missouri"]) + tc(current[
                "montana"]) + tc(
                current["nebraska"]) + tc(current["nevada"]) + tc(current["new hampshire"]) + tc(current["new jersey"]) + tc(current["new mexico"]) + tc(current["new york"]) + tc(current["north carolina"]) + tc(current["north dakota"]) +
              tc(current[
                "ohio"]) + tc(current["oklahoma"]) + tc(current["oregon"]) + tc(current["pennsylvania"]) + tc(current["rhode island"]) + tc(current["south carolina"]) + tc(current["south dakota"]) + tc(current["tennessee"]) + tc(current[
                "texas"]) +
              tc(current["utah"]) + tc(current["vermont"]) + tc(current["virginia"]) + tc(current["washington"]) + tc(current["west virginia"]) + tc(current["canada"]));
            rc -= (tr(current["alabama"]) + tr(current["alaska"]) + tr(current["arizona"]) + tr(current["arkansas"]) + tr(current["california"]) + tr(current["colorado"]) + tr(current["connecticut"]) + tr(current["delaware"]) + tr(current[
                "florida"]) + tr(current["georgia usa"]) + tr(current["hawaii"]) + tr(current["idaho"]) + tr(current["illinois"]) + tr(current["indiana"]) + tr(current["iowa"]) + tr(current["kansas"]) + tr(current["kentucky"]) + tr(current[
                "louisiana"]) + tr(current["maine"]) + tr(current["maryland"]) + tr(current["massachusetts"]) + tr(current["michigan"]) + tr(current["minnesota"]) + tr(current["mississippi"]) + tr(current["missouri"]) + tr(current[
                "montana"]) + tc(
                current["nebraska"]) + tr(current["nevada"]) + tr(current["new hampshire"]) + tr(current["new jersey"]) + tr(current["new mexico"]) + tr(current["new york"]) + tr(current["north carolina"]) + tr(current["north dakota"]) +
              tr(current[
                "ohio"]) + tr(current["oklahoma"]) + tr(current["oregon"]) + tr(current["pennsylvania"]) + tr(current["rhode island"]) + tr(current["south carolina"]) + tr(current["south dakota"]) + tr(current["tennessee"]) + tr(current[
                "texas"]) +
              tr(current["utah"]) + tr(current["vermont"]) + tr(current["virginia"]) + tr(current["washington"]) + tr(current["west virginia"]) + tr(current["canada"]));
            dd -= (td(current["alabama"]) + td(current["alaska"]) + td(current["arizona"]) + td(current["arkansas"]) + td(current["california"]) + td(current["colorado"]) + td(current["connecticut"]) + td(current["delaware"]) + td(current[
                "florida"]) + td(current["georgia usa"]) + td(current["hawaii"]) + td(current["idaho"]) + td(current["illinois"]) + td(current["indiana"]) + td(current["iowa"]) + td(current["kansas"]) + td(current["kentucky"]) + td(current[
                "louisiana"]) + td(current["maine"]) + td(current["maryland"]) + td(current["massachusetts"]) + td(current["michigan"]) + td(current["minnesota"]) + td(current["mississippi"]) + td(current["missouri"]) + td(current[
                "montana"]) + tc(
                current["nebraska"]) + td(current["nevada"]) + td(current["new hampshire"]) + td(current["new jersey"]) + td(current["new mexico"]) + td(current["new york"]) + td(current["north carolina"]) + td(current["north dakota"]) +
              td(current[
                "ohio"]) + td(current["oklahoma"]) + td(current["oregon"]) + td(current["pennsylvania"]) + td(current["rhode island"]) + td(current["south carolina"]) + td(current["south dakota"]) + td(current["tennessee"]) + td(current[
                "texas"]) +
              td(current["utah"]) + td(current["vermont"]) + td(current["virginia"]) + td(current["washington"]) + td(current["west virginia"]) + td(current["canada"]));
          } else if (name == "china") {
            for (const [key, value] of Object.entries(current)) {
              if (datasets[6]["columns"].includes(key)) {
                if (value == undefined) {
                  value = "0"
                };
                items = value.split("-");
                switch (items.length) {
                  case 4:
                    dd += +items[3];
                  case 3:
                    rc += +items[2];
                  case 2:
                    sp += +items[1];
                  case 1:
                    cf += +items[0];
                    break;
                };
                active = cf - dd - rc;
              }
            }
          } else {
            d = current[name];
            if (d == undefined) {
              d = "0"
            };
            items = d.split("-");
            switch (items.length) {
              case 4:
                dd += +items[3];
              case 3:
                rc += +items[2];
              case 2:
                sp += +items[1];
              case 1:
                cf += +items[0];
                break;
            };
            active = cf - dd - rc;
          }
          active = cf - dd - rc;
          place[name].c.push(cf);
          //place[name].s.push(sp);
          place[name].r.push(rc);
          place[name].d.push(dd);
          place[name].a.push(active);
        });
        return place[name];
      }
      //this function take a place name and diaplay the data to the info panel
      function showPlace(name) {
        len = places[name].t.length;
        $(".confirmed-count").text(places[name].c[len - 1].toLocaleString());
        $(".recovered-count").text(places[name].r[len - 1].toLocaleString());
        $(".death-count").text(places[name].d[len - 1].toLocaleString());
        $(".active-count").text(places[name].a[len - 1].toLocaleString());
        nc = places[name].c[len - 1] - places[name].c[len - 2]; //new aggregate confirmed cases of the day
        nr = places[name].r[len - 1] - places[name].r[len - 2]; //new recovered confirmed cases of the day
        nd = places[name].d[len - 1] - places[name].d[len - 2]; //new death of the day
        na = places[name].a[len - 1] - places[name].a[len - 2]; //new active cases of the days
        if (nc > 0) {
          $(".confirmed-new-count").text("+" + nc.toLocaleString());
        } else if (nc == 0) {
          $(".confirmed-new-count").text("");
        } else {
          $(".confirmed-new-count").text(nc.toLocaleString());
        }
        if (nr > 0) {
          $(".recovered-new-count").text("+" + nr.toLocaleString());
        } else if (nr == 0) {
          $(".recovered-new-count").text("")
        } else {
          $(".recovered-new-count").text(nr.toLocaleString());
        }
        if (nd > 0) {
          $(".death-new-count").text("+" + nd.toLocaleString());
        } else if (nd == 0) {
          $(".death-new-count").text("")
        } else {
          $(".death-new-count").text(nd.toLocaleString());
        }
        if (na > 0) { //only display info icon when there's change
          document.getElementById("counticon").style.display = "initial";
          $(".active-new-count").text("+" + na.toLocaleString());
        } else if (na < 0) {
          document.getElementById("counticon").style.display = "initial";
          $(".active-new-count").text("" + na.toLocaleString());
        } else if (na == 0) {
          document.getElementById("counticon").style.display = "none";
          $(".active-new-count").text("")
        } else {
          document.getElementById("counticon").style.display = "none";
          $(".active-new-count").text(na.toLocaleString());
        }
        //add ",CHINA" to every provinces in China
        if (datasets[6]["columns"].includes(name)) { //add ",CHINA" to every provinces in China
          $("#placename").text(name.toUpperCase() + ", CHINA");
          if (name == "taiwan") {
            $("#placename").text("Taiwan");
          }
          if (name == "hongkong") {
            $("#placename").text("Hong Kong");
          }
          if (name == "macau") {
            $("#placename").text("Macau");
          }
        } else {
          $("#placename").text(name.toUpperCase());
        }
        //add reference source for each place
        if (datasets[4]["columns"].includes(name)) {
          $("#source-website").html( //Unisted states
            '<a target="_blank" href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/"> WHO</a>, <a target="_blank" href="https://www.cdc.gov/coronavirus/2019-ncov/cases-updates/cases-in-us.html?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fcases-in-us.html">CDC</a>, <a target="_blank" href="https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html">New York Times</a>, and <a target="_blank" href="https://www.nbcnews.com/health/health-news/coronavirus-u-s-map-where-virus-has-been-confirmed-across-n1124546">NBC News</a>.'
          );
        } else if (datasets[5]["columns"].includes(name)) { //Canada
          $("#source-website").html('<a target="_blank" href="https://www.canada.ca/en/public-health/services/diseases/2019-novel-coronavirus-infection.html">Public Health Agency of Canada.</a>');
        } else if (datasets[6]["columns"].includes(name)) { //China
          $("#source-website").html(
            '<a target="_blank" href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/"> WHO</a>, <a target="_blank" href="http://www.nhc.gov.cn/xcs/xxgzbd/gzbd_index.shtml">China CDC</a>, and <a target="_blank" href="https://voice.baidu.com/act/newpneumonia/newpneumonia">Baidu</a>.'
          );
        } else if (name == "Global Trend") { //global
          $("#source-website").html(
            '<a target="_blank" href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/"> WHO</a>, <a target="_blank" href="https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html">New York Times</a>, <a target="_blank" href="https://www.nbcnews.com/health/health-news/coronavirus-u-s-map-where-virus-has-been-confirmed-across-n1124546">NBC News</a>, <a target="_blank" href="https://www.cdc.gov/coronavirus/2019-ncov/cases-updates/cases-in-us.html?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fcases-in-us.html">CDC</a>, <a target="_blank" href="https://voice.baidu.com/act/newpneumonia/newpneumonia">Baidu</a>, <a target="_blank" href="https://en.wikipedia.org/wiki/2019%E2%80%9320_coronavirus_pandemic">Wikipedia</a>, and etc.'
          );
        } else if (name == "japan") { //japan
          $("#source-website").html(
            '<a target="_blank" href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/"> WHO</a>, <a target="_blank" href="https://en.wikipedia.org/wiki/2019%E2%80%9320_coronavirus_pandemic">Wikipedia</a>, and <a target="_blank" href="https://voice.baidu.com/act/newpneumonia/newpneumonia">Baidu</a>. The discrepancy on the data in Japan between March 11th and March 12th comes from the disagreement of whether to include cases from the Princess Diamond cruise.'
          );
        } else { //Other countries
          $("#source-website").html(
            '<a target="_blank" href="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports/"> WHO</a>, <a target="_blank" href="https://en.wikipedia.org/wiki/2019%E2%80%9320_coronavirus_pandemic">Wikipedia</a>, and <a target="_blank" href="https://voice.baidu.com/act/newpneumonia/newpneumonia">Baidu</a>.'
          );
        }
      }
      //this funciton take a place name and check the status of that place, then fill the background based on its status
      //grey slash for non-case country, zero aggregate confirmed case
      //green slash for country that had cases before but now has zero active confirmed case
      //other countries remain blank background
      function setFill(enname) {
        var pop = datasets[0][datasets[0].length - 1][enname];
        if (pop == "" || pop == undefined || pop.toString().split("-")[0] == "0") {
          return 'url(img/texture-s.png)';
        } else {
          pop = +pop.toString().split("-")[0] - +pop.toString().split("-")[2] - +pop.toString().split("-")[3];
          // return "#00000000";
        }
        if (pop == 0) {
          return 'url(img/texture-sg.png)';
          // return 'url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHdpZHRoPScxMCcgaGVpZ2h0PScxMCc+CiAgPHJlY3Qgd2lkdGg9JzEwJyBoZWlnaHQ9JzEwJyBmaWxsPSd3aGl0ZScgLz4KICA8cmVjdCB4PScwJyB5PScwJyB3aWR0aD0nMScgaGVpZ2h0PScxJyBmaWxsPSdibGFjaycgLz4KPC9zdmc+")';
        } else {
          return 'url()';
        }
      }
      //this function take a place name, return a color that fills the place area on the maps
      //the color is based on the number of active confirmed case
      function setColor(enname) {
        var id = 0;
        var pop = datasets[0][datasets[0].length - 1][enname];
        if (pop != undefined) {
          pop = +pop.toString().split("-")[0] - +pop.toString().split("-")[2] - +pop.toString().split("-")[3]; // remaining confirmed
        } else {
          pop = 0;
          // return "#00000000";
        }
        if (pop >= 50000) {
          id = 5;
        } else if (pop > 10000 && pop <= 50000) {
          id = 4;
        } else if (pop > 5000 && pop <= 10000) {
          id = 3;
        } else if (pop > 1000 && pop <= 5000) {
          id = 2;
        } else if (pop > 100 && pop <= 1000) {
          id = 1;
        } else if (pop > 0 && pop <= 100) {
          id = 0;
        } else {
          id = -1;
          return "#00000000";
        }
        return colors[id];
      }
      //this function takes a place's name, set the color background and opacitiy for the place area on the map
      function style(feature) {
        if (feature.properties.enname == "us" || feature.properties.enname == "canada") {
          return {
            fillOpacity: 0,
            opacity: 0,
          };
        } else {
          return {
            fill: setFill(feature.properties.enname),
            fillColor: setColor(feature.properties.enname),
            fillOpacity: 0.4,
            weight: 0.5,
            opacity: 1,
            color: '#b4b4b4',
            dashArray: '2'
          };
        }
      }
      //this function works when there's a click on the map
      //will highlight the layer that the mouse clicked
      function highlightFeature(e) {
        // e indicates the current event
        var layer = e.target; //the target capture the object which the event associates with
        layer.setStyle({
          weight: 2,
          opacity: 0.8,
          color: '#e3e3e3',
          fillColor: '#00ffd9',
          fillOpacity: 0.1
        });
        // bring the layer to the front.
        layer.bringToFront();
        if (e.target.feature.properties.enname == "us" || e.target.feature.properties.enname == "canada") {
          layer.bringToBack();
        }
      }
      // 3.2.2 zoom to the highlighted feature when the mouse is clicking onto it.
      function zoomToFeature(e) {
        // mymap.fitBounds(e.target.getBounds());
        L.DomEvent.stopPropagation(e);
        $("#hint").text("Click here to the global trend.");
        displayPlace(e.target.feature.properties.enname)
      }
      // 3.2.3 reset the hightlighted feature when the mouse is out of its region.
      function resetHighlight(e) {
        areas.resetStyle(e.target);
      }
      // 3.3 add these event the layer obejct.
      function onEachFeature(feature, layer) {
        layer.on({
          mouseover: highlightFeature,
          click: zoomToFeature,
          mouseout: resetHighlight
        });
      }
      var areas = new L.TopoJSON(datasets[1], {
        style: style,
        onEachFeature: onEachFeature
      }).addTo(mymap);
      //add the control panel at the topright corner of the maps
      //control the display of infection level, cases and commnities icon
      new L.control.layers(baseLayers, {
        "Infection Level": areas,
        "Infection Case(s) &nbsp;&nbsp; <i class='fas fa-users' style='color: #dc3545;'></i>": cases
        //"Infected Community &nbsp;&nbsp; <i class='fas fa-procedures' style='color: #dc3545;'></i>": communities
      }, {
        collapsed: false
      }).addTo(mymap);
      //when click on the tag with "hint" class, the info panel will display global information
      $("#hint").on("click", function() {
        places["Global Trend"] = calPlace("Global Trend");
        showPlace("Global Trend");
        // calCounts(global);
        chart.load({
          columns: [places["Global Trend"].c, places["Global Trend"].a, places["Global Trend"].r, places["Global Trend"].d],
          unload: ['Aggr. Confirmed', 'Active Confirmed', 'Recovered', 'Death'],
        });
        $("#hint").text("Click a place to review local trend.");
      });
      mymap.on('click', onMapClick);

      function onMapClick(e) {
        $("#hint").click();
      }
      places["Global Trend"] = calPlace("Global Trend");
      showPlace("Global Trend");
      //this set the style for the linechart displayed in info panel
      chart = c3.generate({
        size: {
          height: 350,
          width: 460
        },
        data: {
          x: "t",
          y: "confirmed",
          columns: [places["Global Trend"].t, places["Global Trend"].c, places["Global Trend"].a, places["Global Trend"].r, places["Global Trend"].d],
          type: 'line',
          axes: {
            confirmed: 'y'
          },
          colors: {
            'Aggr. Confirmed': '#dc3545',
            // Suspected: 'orange',
            'Active Confirmed': 'orange',
            'Recovered': '#28a745',
            'Death': 'SlateBlue'
          }
        },
        zoom: {
          enabled: true,
          type: "scroll"
        },
        axis: {
          x: {
            type: "timeseries",
            tick: {
              format: "%b %d",
              centered: true,
              fit: true,
              count: 8
            }
          },
          y: {
            label: {
              text: 'Cases',
              position: 'outer-middle'
            },
            min: 0,
            padding: {
              bottom: 0
            },
            tick: {
              format: d3locale.format(",")
            },
            type: 'linear'
          }
        },
        point: {
          r: 3,
          focus: {
            expand: {
              r: 5
            }
          }
        },
        tooltip: {
          linked: true,
        },
        legend: {
          position: 'inset',
          inset: {
            anchor: "top-left",
            y: 0,
            step: 20
          },
        },
        bindto: "#total-chart"
      });
      // var firstLegend = $(".c3-legend-item");
      // var legendCon = $(firstLegend.node().parentNode);
      // var legendY = parseInt(firstLegend.select('text').attr('y'));
      // legendCon
      //   .append('text')
      //   .text('toggle on/off the curve or scroll on the curves to change the date range')
      //   .attr('y', legendY - 20);
      // var firstLegend = d3.select(".c3-legend-item");
      // var legendCon = d3.select(firstLegend.node().parentNode);
      // var legendY = parseInt(firstLegend.select('text').attr('y'));
      // legendCon
      //   .append('text')
      //   .text('toggle on/off the curve or scroll on the curves to change the date range')
      //   .attr('y', legendY - 20);
      //this funtion take a place's name and load the linechart with that place's data
      function displayPlace(name) {
        places[name] = calPlace(name);
        var deck2 = document.getElementById('deck-2')
        if (datasets[4]["columns"].includes(name) | name == "us") {
          deck2.style.visibility = 'hidden';
          deck2.style.height = '0';
          chart.load({
            columns: [places[name].c, places[name].c, places[name].d, places[name].d],
            unload: ['Aggr. Confirmed', 'Active Confirmed', 'Recovered', 'Death'],
          });
        } else {
          deck2.style.visibility = 'visible';
          deck2.style.height = 'auto';
          chart.load({
            columns: [places[name].c, places[name].a, places[name].r, places[name].d],
            unload: ['Aggr. Confirmed', 'Active Confirmed', 'Recovered', 'Death'],
          });
        }
        showPlace(name);
      }
      //this function generate the situational-heatmap table
      function makeTable() {
        var topinuse = {};
        if (document.getElementById('areaSwitcher').checked != false) {
          topinuse = sustop;
        } else {
          topinuse = stop;
        }
        //create rows for each country/state
        Object.keys(topinuse).slice(0, 52).forEach(function(d) {
          if (d.toUpperCase() == "DIAMOND PRINCESS") {
            return;
          }
          var dlabel = d.toUpperCase();
          if (d.toUpperCase() == "GEORGIA USA") {
            dlabel = "GEORGIA";
          }
          $("tbody").append("<tr id='" + d.replace(" ", "") + "-row'><th style='text-align:right;cursor: pointer; width:350px !important'>" + dlabel + "</th></tr>");
          places[d] = calPlace(d);
          //aggregate confirm column
          $("tr#" + d.replace(" ", "") + "-row").append('<th style="text-align:right"><i class="cell-' + d.replace(" ", "") + '-aggre-confirmed">' + places[d].c[len - 1].toLocaleString() + '</i></th>');
          $("tr#" + d.replace(" ", "") + "-row").append('<th ><i class="cell-' + d.replace(" ", "") + '">' + "" + '</i></th>');
          var a = [];
          for (var i = len - showLen; i < len; i++) {
            a.push(places[d].a[i]);
          }
          $("." + 'cell-' + d.replace(" ", "")).sparkline(a, {
            type: 'line',
            lineColor: '#bf0000',
            fillColor: '#ffd4aa',
            disableTooltips: true
          });
          //place blocks into each cell based on the that day's data
          for (var i = len - showLen - 1; i < len; i++) {
            // a.push(places[d].a[i]);
            //$("tr#" + d.replace(" ", "") + "-row").append('<th scope="col"><i class="cell">' + places[d].c[i] + '</i></th>');
            $("tr#" + d.replace(" ", "") + "-row").append('<th ><i class="cell cell-' + d.replace(" ", "") + '-' + i.toString() + '">' + "" + '</i></th>');
            bgcolor = "#28a745";
            bdcolor = "#28a745";
            size = "32px";
            bdsize = "0px";
            top = "0rem";
            left = "0rem";
            //all the cases are recovered
            // c ===> 0, 10, 100, 1000, 10000
            // size =>0,  4,   8,   16,    32
            if (places[d].a[i] >= 10000) {
              size = "32px"
              top = "-.45rem";
              left = "-.35rem";
            } else if (places[d].a[i] < 10000 && places[d].a[i] >= 1000) {
              size = "24px";
              top = "-.2rem";
              left = "-.1rem";
            } else if (places[d].a[i] < 1000 && places[d].a[i] >= 100) {
              size = "16px";
              top = "0rem";
              left = ".1rem";;
            } else if (places[d].a[i] < 100 && places[d].a[i] >= 10) {
              size = "10px";
              top = ".25rem";
              left = ".25rem";
            } else if (places[d].a[i] < 10 && places[d].a[i] >= 1) {
              size = "8px";
              top = ".25rem";
              left = ".25rem";
            } else {
              size = "0px";
              bdsize = "0px";
            }
            // a/c rate ==> red, oregen, yellow, green{plus yellow}
            // color ==>  recover:  #28a745
            // a ===>
            acrate = places[d].a[i] / places[d].c[i]
            colors = chroma.scale('YlOrRd').mode('lch').colors(6);
            if (acrate > 0.995) {
              bgcolor = colors[5];
            } else if (acrate >= 0.9 && acrate <= 0.995) {
              bgcolor = colors[4];
            } else if (acrate >= 0.5 && acrate <= 0.9) {
              bgcolor = colors[3];
            } else if (acrate >= 0.3 && acrate <= 0.5) {
              bgcolor = colors[2];
            } else if (acrate >= 0.2 && acrate <= 0.3) {
              bgcolor = colors[1];
            } else if (acrate < 0.2 && places[d].c[i] > 100) {
              bgcolor = '#28a745';
            } else {
              bgcolor = colors[1];
            }
            $('.cell-' + d.replace(" ", "") + '-' + i.toString())
              .css("background-color", bgcolor)
              .css("border", bdsize + " solid " + bdcolor)
              .css("width", size)
              .css("height", size)
              .css("margin-top", top)
              .css("margin-left", left);
          }
          //when lick on a country's row, the info panel will show the information related to that country/place
          $("tr#" + d.replace(" ", "") + "-row").on("click", function() {
            // places[d] = calPlace(d);
            var deck2 = document.getElementById('deck-2')
            if (datasets[4]["columns"].includes(d)) {
              deck2.style.visibility = 'hidden';
              deck2.style.height = '0';
              chart.load({
                columns: [places[d].c, places[d].c, places[d].d, places[d].d],
                unload: ['Aggr. Confirmed', 'Active Confirmed', 'Recovered', 'Death'],
              });
            } else {
              deck2.style.visibility = 'hidden';
              deck2.style.height = '0';
              chart.load({
                columns: [places[d].c, places[d].a, places[d].r, places[d].d],
                unload: ['Aggr. Confirmed', 'Active Confirmed', 'Recovered', 'Death'],
              });
            }
            showPlace(d);
          })
        })
      }
      //switch to show the situational-heatmap feature
      $('#areaSwitcher').change(function() {
        $('.loader').show();
        $("#rankingToggle").css('visibility', 'visible');
        $("#table").css("visibility", "visible");
        $(".leaflet-control-container").css("visibility", "hidden");
        len = places["Global Trend"].t.length
        showLen = 20
        $("thead").html('<th scope="col" style="text-align:right; width:200px !important"><b>State</b></th>');
        $("thead").append("<th style='text-align:center' >Aggr. Cfm </th>");
        $("thead").append("<th style='text-align:center' >Active Cfm. Trend</th>");
        Object.values(places["Global Trend"].t.slice(len - 1 - showLen, len)).forEach(function(d) {
          label = (new Date(d)).toString().substring(4, 10);
          $("thead").append("<th style='text-align:center' >" + label + "</th>");
        });
        $("tbody").html('');
        makeTable();
        $('.loader').fadeOut("slow");
      })
      //swithch between us and global heatmap
      $('#panelSwitcher').change(function() {
        $('.loader').show();
        //this part of content will shall when it's on global heatmap
        if (document.getElementById('panelSwitcher').checked == false) {
          $("#table").css("visibility", "hidden");
          $("#rankingToggle").css("visibility", "hidden");
          $(".leaflet-control-container").css("visibility", "visible");
          $("#content-explain").text(
            "In the main map, an country or region's inflection level is measured by the # of today's active/remaining confirmed cases. The gray slash texture indicates that no previous cases are discovered; the green slash texture  indicates the region in which all the infected cases has recovered (or passed away)."
          );
          $("thead").html('');
          $("tbody").html('');
        } else { //this part of content will shall when it's on us heatmap
          $("#rankingToggle").css('visibility', 'visible');
          $("#content-explain").text(
            "This situational heatmap (Beta) illustrates the rank of active confirmed cases in all countries or U.S. states in the descending order. It uses a series of blocks in different size and color to represent the number and recover rate of coronavirus cases of different places within the last 20 days. The size of the block increases as the number of active confirmed case increases. While the color of the block, in a \"yellow-orange-red\" ramp, gets darker as the 'active / aggregate' rate (a.k.a recover rate) increases."
          );
          $("#table").css("visibility", "visible");
          $(".leaflet-control-container").css("visibility", "hidden");
          $("#rankingText").remove();
          $("#rankingIcon").remove();
          $("#rankingSpace").remove();
          len = places["Global Trend"].t.length
          showLen = 20
          $("thead").html('<th scope="col" style="text-align:right; width:250px !important"><b>Country</b></th>');
          $("thead").append("<th style='text-align:center' >Aggr. Cfm </th>");
          $("thead").append("<th style='text-align:center' >Active Cfm. Trend</th>");
          Object.values(places["Global Trend"].t.slice(len - 1 - showLen, len)).forEach(function(d) {
            //label = new Date(new Date(d).setHours(new Date(d).getHours() + 8)).toString().substring(4,10);
            label = (new Date(d)).toString().substring(4, 10);
            // console.log(label);
            $("thead").append("<th style='text-align:center;' >" + label + "</th>");
          });
          $("tbody").html('');
          makeTable();
        }
        $('.loader').fadeOut("slow");
      })
      $(".leaflet-control-attribution")
        .css("background-color", "transparent")
        .html("");
    });
    /* When the user clicks on the button,
    toggle between hiding and showing the dropdown content */
    $('.dropdown-toggle').dropdown()
    $("#logarithm").on("click", function() {
      chart.internal.config.axis_y_tick_format = d3.format(",.2r");
      $(".chart-legend").css({
        "left": "140px",
        "width": "325px"
      });
      $(".dropdown-toggle").text('logarithm option');
      chart.axis.types({
        y: 'log',
      });
    });
    $("#linear").on("click", function() {
      $(".chart-legend").css({
        "left": "120px",
        "width": "345px"
      });
      $(".dropdown-toggle").text('linear option');
      chart.axis.types({
        y: 'linear',
      });
    });
  </script>

  <!-- pop-up notice window -->
  <!-- <script>
    $('#overlay').modal('show');
  </script> -->

  <!-- Google Analytics -->
  <script>
    window.ga = window.ga || function() {
      (ga.q = ga.q || []).push(arguments)
    };
    ga.l = +new Date;
    ga('create', 'UA-100818948-4', 'auto');
    ga('send', 'pageview');
  </script>
  <script async src='https://www.google-analytics.com/analytics.js'></script>

  <script>
    window.ga = window.ga || function() {
      (ga.q = ga.q || []).push(arguments)
    };
    ga.l = +new Date;
    ga('create', 'UA-159947082-1', 'auto');
    ga('send', 'pageview');
  </script>
  <script async src='https://www.google-analytics.com/analytics.js'></script>
  <!-- Google Analytics End-->
</body>

</html>
  
