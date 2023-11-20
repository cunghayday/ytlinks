# Extract Youtube URL form HTML source
Tool write by HTML and JavaScript, extract Youtube URL to HTML web source.<br>
You can get HTML source by Inspect web page (F12) of Firefox or Chrome, don't use view source (Ctrl + U) because many Youtube URL display after Javascipt code execute.<br>
Download ytlinks.html and open by web browser or upload to web hosting.<br>
Put HTML source to top textarea then press Extract button.<br>

<p><textarea id="input" rows="4" cols="50" style="max-width: 96%;"></textarea></p>
<button onclick="doit()">Tách</button>&nbsp;
<button onclick="copy()">Chép</button>&nbsp;
<button onclick="clearit()">Xoá</button>
<p><textarea id="output" rows="8" cols="50" style="max-width: 96%;"></textarea></p>
<p id="nlinks"></p>


<script>

let nlinks = 0;
function copy() {
	  var copyText = document.getElementById("output");
	  copyText.select();
	  copyText.setSelectionRange(0, 99999)
	  document.execCommand("copy");
	  navigator.clipboard.writeText(copyText.value);
	}
function clearit() {	
document.getElementById("input").value = '';
document.getElementById("output").value = '';
document.getElementById("nlinks").innerHTML = '';
}
function removeDuplicates(arr) { 
    return arr.filter((item, 
        index) => arr.indexOf(item) === index); 
} 
function doit() {
let text = document.getElementById("input").value;
let result1 = text.match(/watch\?v=[a-zA-Z0-9\-_]+/g);
var result2 = removeDuplicates(result1);
var result3 = result2.map(function(ytlink) { 
  return 'https://www.youtube.com/' + ytlink; 
})
nlinks =  result3.length;
let output = result3.join('\n');
document.getElementById("output").value = output;
document.getElementById("nlinks").innerHTML = 'Đã tách được <span style="font-weight:bold;">' + nlinks + '</span> liên kết.';
}
 
</script>
