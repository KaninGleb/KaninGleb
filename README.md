<!-- Codewars badge -->
[![Codewars badge](https://www.codewars.com/users/KaninGleb/badges/large)](https://www.codewars.com/users/KaninGleb)

<!-- Profile views -->
<div style="border: 5px solid black;">
    <img src="https://komarev.com/ghpvc/?username=KaninGleb&abbreviated=true&style=for-the-badge&color=fe428e" alt="Profile Views" style="border-radius: 10px; width: 160px; height: auto;"/>
</div>

<?php

// disable cache so that the image will be fetched every time
$timestamp = gmdate("D, d M Y H:i:s") . " GMT";
header("Expires: $timestamp");
header("Last-Modified: $timestamp");
header("Pragma: no-cache");
header("Cache-Control: no-cache, must-revalidate");

// set the content type to be an image
header("Content-type: image/svg+xml");

// increment the file and return the current number
function incrementFile($filename): int
{
    // if the file exists
    if (file_exists($filename)) {
        // open the file for reading and writing
        $fp = fopen($filename, "r+") or die("Failed to open the file.");
        // lock the file so it can't be opened by another user
        flock($fp, LOCK_EX);
        // read the file and add 1
        $count = fread($fp, filesize($filename)) + 1;
        // delete the contents
        ftruncate($fp, 0);
        // go to the beginning of the file
        fseek($fp, 0);
        // write the new count
        fwrite($fp, $count);
        // unlock the file
        flock($fp, LOCK_UN);
        // close the file
        fclose($fp);
    }
    // create the file if it doesn't exist
    else {
        // set the contents of the file to the number 1
        $count = 1;
        file_put_contents($filename, $count);
    }
    // return the current file contents
    return $count;
}

// short numbers from https://stackoverflow.com/a/52490452/11608064
function shortNumber($num)
{
    $units = ['', 'K', 'M', 'B', 'T'];
    for ($i = 0; $num >= 1000; $i++) {
        $num /= 1000;
    }
    return round($num, 1) . $units[$i];
}

// get contents of a URL with curl
function curl_get_contents($url): string
{
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_HEADER, 0);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
    curl_setopt($ch, CURLOPT_VERBOSE, 0);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
    $response = curl_exec($ch);
    curl_close($ch);
    return $response;
}

// increment the file and get the current count
$message = incrementFile("views.txt");

// set parameters for the shields.io URL
$params = [
    "label" => "Views",
    "logo" => "github",
    "message" => shortNumber($message),
    "color" => "purple",
    "style" => "for-the-badge"
];

// build the URL with an SVG image of the view counter
$url = "https://img.shields.io/static/v1?" . http_build_query($params);

// output the response (svg image)
echo curl_get_contents($url);

<!-- GitHub stats with streak-->
## :fire: My Stats:
[![GitHub Streak](https://github-readme-streak-stats.herokuapp.com?user=KaninGleb&theme=radical&border_radius=10&date_format=M%20j%5B%2C%20Y%5D)](https://git.io/streak-stats)

<!-- GitHub stats -->
## :zap: My Dev Statistics:
<p>
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=KaninGleb&show_icons=true&theme=radical&border_radius=10" />&nbsp;
<img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=KaninGleb&exclude_repo=KNN-Image-Classification&show_icons=true&border_radius=10&layout=compact&langs_count=8&theme=radical"/>
</p>
