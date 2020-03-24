<html lang="en"><head>
<meta charset="UTF-8">
<link rel="apple-touch-icon" type="image/png" href="https://static.codepen.io/assets/favicon/apple-touch-icon-5ae1a0698dcc2402e9712f7d01ed509a57814f994c660df9f7a952f3060705ee.png">
<meta name="apple-mobile-web-app-title" content="CodePen">
<link rel="shortcut icon" type="image/x-icon" href="https://static.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico">
<link rel="mask-icon" type="" href="https://static.codepen.io/assets/favicon/logo-pin-8f3771b1072e3c38bd662872f6b673a722f4b3ca2421637d5596661b4e2132cc.svg" color="#111">
<title>CodePen - Packery Infinite-Scroll Images-Loaded JSON Scrolling Image Gallery giong Hover Menu Settings localStorage Categories Pluggable</title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
/* Gallery Start */
body {
    font-family: sans-serif;
    line-height: 1.4;
    padding: 10px;
    max-width: 100%;
    width: 100%;
    margin: 0 auto;
	background-color: black;
	color: white;
	overflow-x: hidden;
}
.madeby {
    position: absolute;
    right: 50px;
    top: 10px;    
}
.grid {
    width: 100%;
}
.grid__col-sizer,
.photo-item {
    /* width: 24%; */
}
.grid.masonry .grid__col-sizer,
.grid.masonry .photo-item {
    width: 24%;
}
.grid__gutter-sizer {
    width: 1%;
}
.photo-item {
    margin-bottom: 10px;
    float: left;
}
.photo-item__image {
    display: block;
    max-width: 100%;
}
.photo-item__caption {
    position: absolute;
    left: 10px;
    bottom: 10px;
    margin: 0;
}
.photo-item__caption a {
    color: white;
    font-size: 0.8em;
    text-decoration: none;
}
.page-load-status {
    display: none; /* hidden by default */
    padding-top: 20px;
    border-top: 1px solid #ddd;
    text-align: center;
    color: #777;
}
/* loader ellips in separate pen CSS */
.loader-ellips {
    font-size: 20px; /* change size here */
    position: relative;
    width: 4em;
    height: 1em;
    margin: 10px auto;
}
.loader-ellips__dot {
    display: block;
    width: 1em;
    height: 1em;
    border-radius: 0.5em;
    background: #555; /* change color here */
    position: absolute;
    animation-duration: 0.5s;
    animation-timing-function: ease;
    animation-iteration-count: infinite;
}
.loader-ellips__dot:nth-child(1),
.loader-ellips__dot:nth-child(2) {
    left: 0;
}
.loader-ellips__dot:nth-child(3) {
    left: 1.5em;
}
.loader-ellips__dot:nth-child(4) {
    left: 3em;
}
@keyframes reveal {
    from {
        transform: scale(0.001);
    }
    to {
        transform: scale(1);
    }
}
@keyframes slide {
    to {
        transform: translateX(1.5em);
    }
}
.loader-ellips__dot:nth-child(1) {
    animation-name: reveal;
}
.loader-ellips__dot:nth-child(2),
.loader-ellips__dot:nth-child(3) {
    animation-name: slide;
}
.loader-ellips__dot:nth-child(4) {
    animation-name: reveal;
    animation-direction: reverse;
}
/* Gallery End */

/* Menu Start */
body,
html {
	margin: 0;
	padding: 0;
	width: 100%;
	height: 100%;
	background-color: #26394e;
}
#menu {
	height: 100%;
	position: fixed;
	background-color: #fed057;
	width: 300px;
	transition: 1000ms all cubic-bezier(0.19, 1, 0.22, 1);
	transform: translateX(-100%);
	left: 60px;
}
#menu.expanded {
	transform: translateX(0%);
	left: 0px;
}
.menu-inner {
	width: 100%;
	height: 100%;
	position: relative;
}
#blob {
	top: 0;
	z-index: -1;
	right: 60px;
	transform: translateX(100%);
	height: 100%;
	position: absolute;
}
#blob-path {
	height: 100%;
	fill: #fed057;
}
.hamburger {
	right: 20px;
	position: absolute;
	width: 20px;
	height: 20px;
	margin-top: -10px;
}
.hamburger .line {
	width: 100%;
	height: 4px;
	background-color: #fff;
	position: absolute;
}
.hamburger .line:nth-child(2) {
	top: 50%;
	margin-top: -2px;
}
.hamburger .line:nth-child(3) {
	bottom: 0;
}
h1 {
	position: fixed;
	right: 0;
	margin: 0;
}
ul {
	padding: 0;
	list-style: none;
	width: 80%;
	margin-left: 10%;
	position: absolute;
	top: 10px;
}
ul li {
	color: #fff;
	font-family: sans-serif;
	padding: 20px 0;
}
h2 {
	position: absolute;
	left: 50%;
	color: #fff;
	margin: 0;
	font-size: 16px;
	font-family: sans-serif;
	font-weight: 100;
}

/* Menu End */
</style>
<script>
  window.console = window.console || function(t) {};
</script>
<script>
  if (document.location.search.match(/type=embed/gi)) {
    window.parent.postMessage("resize", "*");
  }
</script>
</head>
<body translate="no">

<div id="menu">
<div class="hamburger" style="transform: translate(120px, 294.562px);">
<div class="line"></div>
<div class="line"></div>
<div class="line"></div>
</div>
<div class="menu-inner">
<ul>
<li>Family</li>
<li>GIFs</li>
<li>Images</li>
<li>Wallpapers</li>
<li>Anime</li>
<li>..Other</li>
</ul>
</div>
<svg version="1.1" id="blob" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="width: 180px;"><path id="blob-path" d="M60,591H0V0h60v94.56241959717482c0,160,119.9999999999999,160,119.9999999999999,200S60,294.5624195971748,60,694.5624195971748V591z"></path></svg>
</div>



<h1>Imagini Arcanum</h1>


<div id="photo-grid" class="grid packery" style="position: relative; height: 0px;">
<div class="grid__col-sizer"></div>
<div class="grid__gutter-sizer"></div>
</div>
<div class="page-load-status" style="display: block;">
<div class="loader-ellips infinite-scroll-request" style="display: none;">
<span class="loader-ellips__dot"></span>
<span class="loader-ellips__dot"></span>
<span class="loader-ellips__dot"></span>
<span class="loader-ellips__dot"></span>
</div>


</div>
<script type="text/html" id="photo-item-template">
	<div class="photo-item" id="img-{{file.name}}" width="{{size.width}}" height="{{size.height}}">
		<img class="photo-item__image" src="{{type}}/{{file.src}}" alt="Photo by {{file.name}}" width="{{size.width}}" height="{{size.height}}" />
			<p class="photo-item__caption">
				{{file.name}}
	</p>
	</div>
</script>

<script src="https://static.codepen.io/assets/common/stopExecutionOnTimeout-157cd5b220a5c80d4ff8e0e70ac069bffd87a61252088146915e8726e5d9f147.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="https://unpkg.com/infinite-scroll@3/dist/infinite-scroll.pkgd.js"></script>
<script src="https://unpkg.com/packery@2/dist/packery.pkgd.min.js"></script>
<script src="https://unpkg.com/masonry-layout@4/dist/masonry.pkgd.js"></script>
<script src="https://unpkg.com/isotope-layout@3/dist/isotope.pkgd.min.js"></script>
<script src="https://unpkg.com/imagesloaded@4/imagesloaded.pkgd.min.js"></script>
<script id="rendered-js">
var gridType = 'packery'; // masonry packery or isotope
var pageType = 'family'; // gifs images or wallpapers
//if (pageType == 'family') gridType = 'masonry';
$('#photo-grid').addClass(gridType);
function pageScroll() {
  window.scrollBy(0, 4); // horizontal and vertical scroll increments
  scrolldelay = setTimeout('pageScroll()', 100); // scrolls every 100 milliseconds
}
if (gridType == 'masonry') {
  var $grid = $(".grid").masonry({
    itemSelector: ".photo-item",
    columnWidth: ".grid__col-sizer",
    gutter: ".grid__gutter-sizer",
    percentPosition: false,
    stagger: 30,
    visibleStyle: { transform: "translateY(0)", opacity: 1 }, // nicer reveal transition
    hiddenStyle: { transform: "translateY(100px)", opacity: 0 } });

  var gridInsance = $grid.data("masonry"); // get Masonry instance
} else if (gridType == 'packery') {
  var $grid = $(".grid").packery({
    itemSelector: ".photo-item",
    gutter: ".grid__gutter-sizer",
    percentPosition: false,
    stagger: 30,
    visibleStyle: { transform: "translateY(0)", opacity: 1 }, // nicer reveal transition
    hiddenStyle: { transform: "translateY(100px)", opacity: 0 } });

  var gridInsance = $grid.data("packery"); // get Packery instance
} else if (gridType == 'isotope') {
  var $grid = $(".grid").isotope({
    layoutMode: 'fitRows', // masonry fitRows cellsByRow vertical packery masonryHorizontal fitColumns cellsByColumn horiz
    itemSelector: ".photo-item",
    gutter: ".grid__gutter-sizer",
    percentPosition: false,
    stagger: 30,
    visibleStyle: { transform: "translateY(0)", opacity: 1 }, // nicer reveal transition
    hiddenStyle: { transform: "translateY(100px)", opacity: 0 } });

  var gridInsance = $grid.data("isotope"); // get Packery instance
}
$grid.infiniteScroll.imagesLoaded = imagesLoaded;
$grid.infiniteScroll({
  path: function () {
    return "photos-api.php?type=" + pageType + "&page=" + this.pageIndex;
  },
  responseType: "text", // load response as flat text
  outlayer: gridInsance,
  status: ".page-load-status",
  history: false });

$grid.on("load.infiniteScroll", function (event, response) {
  var data = JSON.parse(response); // parse response into JSON data
  var itemsHTML = data.map(getItemHTML).join(""); // compile data into HTML
  var $items = $(itemsHTML); // convert HTML string into elements
  $items.imagesLoaded(function () {// append item elements
    if (gridType == 'masonry') {
      $grid.infiniteScroll("appendItems", $items).masonry("appended", $items);
    } else if (gridType == 'packery') {
      $grid.infiniteScroll("appendItems", $items).packery("appended", $items);
    } else if (gridType == 'isotope') {
      $grid.infiniteScroll("appendItems", $items).isotope("appended", $items);
    }
    if ($('.photo-item').length < 50)
    $grid.infiniteScroll("loadNextPage"); // load initial pag
  });
});
$grid.infiniteScroll("loadNextPage"); // load initial page
var itemTemplateSrc = $("#photo-item-template").html();
function getItemHTML(photo) {
  return microTemplate(itemTemplateSrc, photo);
}
function microTemplate(src, data) {// micro templating, sort-of
  return src.replace(/\{\{([\w\-_\.]+)\}\}/gi, function (match, key) {// replace {{tags}} in source
    var value = data; // walk through objects to get value
    key.split(".").forEach(function (part) {
      value = value[part];
    });
    return value;
  });
}
pageScroll();


/* svg gooey hover menu start */
$(window).load(function () {
  var height = window.innerHeight,
  x = 0,
  y = height / 2,
  curveX = 10,
  curveY = 0,
  targetX = 0,
  xitteration = 0,
  yitteration = 0,
  menuExpanded = false;
  blob = $("#blob"),
  blobPath = $("#blob-path"),
  hamburger = $(".hamburger");
  $(this).on("mousemove", function (e) {
    x = e.pageX;
    y = e.pageY;
  });
  $(".hamburger, .menu-inner").on("mouseenter", function () {
    $(this).parent().addClass("expanded");
    menuExpanded = true;
  });
  $(".menu-inner").on("mouseleave", function () {
    menuExpanded = false;
    $(this).parent().removeClass("expanded");
  });
  function easeOutExpo(currentIteration, startValue, changeInValue, totalIterations) {
    return changeInValue * (-Math.pow(2, -10 * currentIteration / totalIterations) + 1) + startValue;
  }
  var hoverZone = 150;
  var expandAmount = 20;
  function svgCurve() {
    if (curveX > x - 1 && curveX < x + 1) {
      xitteration = 0;
    } else {
      if (menuExpanded) {
        targetX = 0;
      } else {
        xitteration = 0;
        if (x > hoverZone) {
          targetX = 0;
        } else {
          targetX = -((60 + expandAmount) / 100 * (x - hoverZone));
        }
      }
      xitteration++;
    }
    if (curveY > y - 1 && curveY < y + 1) {
      yitteration = 0;
    } else {
      yitteration = 0;
      yitteration++;
    }
    curveX = easeOutExpo(xitteration, curveX, targetX - curveX, 100);
    curveY = easeOutExpo(yitteration, curveY, y - curveY, 100);
    var anchorDistance = 200;
    var curviness = anchorDistance - 40;
    var newCurve2 = "M60," + height + "H0V0h60v" + (curveY - anchorDistance) + "c0," + curviness + "," + curveX + "," + curviness + "," + curveX + "," + anchorDistance + "S60," + curveY + ",60," + (curveY + anchorDistance * 2) + "V" + height + "z";
    blobPath.attr("d", newCurve2);
    blob.width(curveX + 60);
    hamburger.css("transform", "translate(" + curveX + "px, " + curveY + "px)");
    $("h2").css("transform", "translateY(" + curveY + "px)");
    window.requestAnimationFrame(svgCurve);
  }
  window.requestAnimationFrame(svgCurve);
});
/* svg gooey hover menu end */
//# sourceURL=pen.js
    </script>


</body></html>
