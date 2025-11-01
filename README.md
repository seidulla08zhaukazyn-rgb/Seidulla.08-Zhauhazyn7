// main.js

var $ajaxUtils = {};

$ajaxUtils.sendGetRequest = function(requestUrl, responseHandler) {
    var request = new XMLHttpRequest();
    request.onreadystatechange = function() {
        if (request.readyState === 4 && request.status === 200)
            responseHandler(request.responseText);
    };
    request.open("GET", requestUrl, true);
    request.send(null);
};

// Load home page content when document is ready
document.addEventListener("DOMContentLoaded", function(event) {
    $ajaxUtils.sendGetRequest("snacks/snacks.json", function(responseText){
        var snacks = JSON.parse(responseText);
        buildAndShowMenuHTML(snacks);
    });
});

function buildAndShowMenuHTML(snacks) {
    var menuHtml = "<ul>";
    for (var i = 0; i < snacks.length; i++) {
        menuHtml += "<li>" + snacks[i].name + "</li>";
    }
    menuHtml += "</ul>";
    document.querySelector("#main-content").innerHTML = menuHtml;
}
