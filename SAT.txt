// ==UserScript==
// @name         SAT-Self Audit Tool
// @namespace    http://tampermonkey.net/
// @version      1.3
// @description  Self validation/audit tool using tampermonkey
// @author       Raghul P R | https://github.com/RaghulRaju
// @match        <Enter the URL> 
// @grant        none
// ==/UserScript==
 
var $ = window.jQuery;
(function() {
    'use strict';
    var now = new Date();
var millisTill10 = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 8,30, 0, 0) - now;
if (millisTill10 < 0) {
     millisTill10 += 86400000; // Enter the data to validate.
}
setTimeout(function(){alert("Enter the data to validate!!")}, millisTill10);
    // Creating data Input box for User to enter the data
    var versionInput = '<div><label>Data: </label><input type="text" id="version"></div>';
    $(versionInput).insertBefore('#groupContainer');
 
    //Get the value from local Storage and place it in the input box
    $('#version').val(localStorage.getItem('version'));
 
    // Initially set the data value to be localStorage Value.
    var version = localStorage.getItem('version');
 
    //Copy the data that the user types in the input box
    $('#version').on('keyup', function() {
        if (this.value.length > 1) {
            version = this.value.trim();
            window.localStorage.setItem("version", version);
        }
      document.getElementById("addResultSubmit").onclick = function click() {
        var value = $('#addResultVersion').val().trim();
        //console.log(value, version);
        if(value !== version ) {
            alert("Invalid Version\nToday's Version is: "+ version);
            setTimeout(function() {$('.editChange').first()[0].childNodes[1].onclick(); }, 3000);
            return false;
        }}
    });
 
    document.getElementById("addResultSubmit").onclick = function click() {
        var value = $('#addResultVersion').val().trim();
        //console.log(value, version);
        if(value !== version ) {
            alert("Invalid Version\nToday's Version is: "+ version);
            setTimeout(function() {$('.editChange').first()[0].childNodes[1].onclick(); }, 3000);
            return false;
        }
    document.getElementById("addResultSubmit").onclick = function click() {
        if ($('#addResultStatus').val() === "5" || $('#addResultStatus').val() === "2" || $('#addResultStatus').val() === "8" || $('#addResultStatus').val() === "11") {
            if(!$('#addResultDefects').val().trim()) {
                alert('Defect Id not Tagged | Please tag a valid defect ID');
                setTimeout(function() {$('.editChange').first()[0].childNodes[1].onclick(); }, 3000);
                return false;
            }
        }
 
    }
}
}
)();