core command in linus whois $ip  | grep -i country

<?php 
$ip = $_GET['ip']; 
if($ip!='') 
{ 
    $country = exec("whois $ip  | grep -i country"); 
    $country = strtolower($country); 
    $country = str_replace("country:", "", "$country"); 
    $country = str_replace("Country:", "", "$country"); 
    $country = str_replace("Country :", "", "$country"); 
    $country = str_replace("country :", "", "$country"); 
    $country = str_replace("network:country-code:", "", "$country"); 
    $country = str_replace("network:Country-Code:", "", "$country"); 
    $country = str_replace("Network:Country-Code:", "", "$country"); 
    $country = str_replace("network:organization-", "", "$country"); 
    $country = str_replace("network:organization-usa", "us", "$country"); 
    $country = str_replace("network:country-code;i:us", "us", "$country"); 
    $country = str_replace("eu#countryisreallysomewhereinafricanregion", "af", "$country"); 
    $country = str_replace("", "", "$country"); 
    $country = str_replace("countryunderunadministration", "", "$country"); 
    $country = str_replace(" ", "", "$country"); 
    if($country) 
    { 
            $image =  'famfamfam-countryflags/'.$country.'.gif'; 
            Header("Content-Type: image/gif"); 
            $fn=fopen($image,"r"); 
            fpassthru($fn); 
    }                         
} 
?>