############################PRACTICAL EXERCISE REGEX############################
#Create a function that extracts your current IP, Subnet and Gateway and outputs them in the following format:
#PS> Get-netinfo
#IP: 192.168.0.1
#Subnet: 255.255.255.0
#Gateway: 192.168.1.1


$ip = ipconfig | ? { $_ -match 'Ipv4.*: ((\d{1,3}\.){3}\d{1,3})' }| select @{n="IPv4";e={$Matches[1]}}


Function Get-netinfo(){
    Begin {
    
    $pattern = '.*?((\d{1,3}\.){3}\d{1,3})'
    $netinfo = ipconfig
    
    $ip = $netinfo -match "IPV4$pattern" | foreach-object{if ($_ -match $pattern) {$matches[1]}}
    $subnet = $netinfo -match "Subnet$pattern" | foreach-object{if ($_ -match $pattern) {$matches[1]}}
    $gw = $netinfo -match "Gateway$pattern" | foreach-object{if ($_ -match $pattern) {$matches[1]}}
    }
    Process {

    }
    End {
    "IP: {0}" -f $ip
    "Subnet: {0}" -f $subnet
    "Gateway: {0}" -f $gw
    }
}

#Create a function that extracts all the URLs found in the file "dns.txt" and outputs URLs, the amount of times the URL 
#is found in the file and the total amount of URLs found.


function get-urlinfo {
    $file = get-content .\dns.txt
    #$regex = '(www\.[a-zA-Z0-9\-\.]+\.(com|org|net))'
    #$regex = '(w{3}\.)(?<=[a-z]\.)(c-m){3}'
    $regex = '([a-zA-Z0-9\-\.]+\.(com|org|net))'
    foreach($line in $file) {
        if($line -match $regex) {
        $matches[1]
        }
    }

}



.\
############################END############################
############################SPLIT AND JOIN############################
'8.8.8.8'.split(".")
1,2,3,4,5 -join "."

'1.8.82.28'.split(".")[0]
############################END############################

############################################################END############################################################
############################################################DAY 4#############################################################
############################1############################

<# 1 #>
function q1($var1,$var2,$var3,$var4) {
    <# Return the product of the arguments #>
    $prod $var1 * $var2 * $var3 * $var4
    $prod
}
#instructor solution
function q1($var1,$var2,$var3,$var4) {
    <# Return the product of the arguments #>
    $prod = $var1 * $var2 * $var3 * $var4
    $prod
}

############################2############################


function q2($arr,$rows,$cols,$key) {
    <# Search the 2 dimensional array for the first occurance of key at column index 0
       and return the value at column index 9 of the same row.
       Return -1 if the key is not found.
    #>
    foreach($i in $arr){
    if($i[0] -eq $key){
    return $i[9]
    }
    elseif($i -ne $key -and $i -eq $arr[-1]){
    return -1
    }

    }
    return -1
    
    #$arr[8]
    #$key
    #$rows
    #$cols
}

#instructor solution
function q2($arr,$rows,$cols,$key) {
    <# Search the 2 dimensional array for the first occurance of key at column index 0
       and return the value at column index 9 of the same row.
       Return -1 if the key is not found.
    #>
    foreach($row in $arr){
      if($row[0] -eq $key){
        return $row[9]
      }
    }
    return -1
}
############################3############################

function q3 {
    <# In a loop, prompt the user to enter positive integers one at time.
       Stop when the user enters a -1. Return the maximum positive
       value that was entered."
	#>
    $numbers = @()
    $number = 0
    while($number -gt -1){
        $number = read-host "input a number"
        $numbers += $number
        $maxvalue = ($numbers | measure-object -maximum).maximum
        if($number -lt 0){
            $maxvalue
            continue
        }

    }


}

#instructor solution
function q3 {
    <# In a loop, prompt the user to enter positive integers one at time.
       Stop when the user enters a -1. Return the maximum positive
       value that was entered."
	#>
$vals = @()
do {
$val = read-host
if($val -ne -1){
$vals += $val
}
} until($val -eq -1)
return ($vals | measure-object -maximum).maximum
}

############################4############################


function q4($filename,$whichline) {
    <# Return the line of text from the file given by the `$filename
	   argument that corresponds to the line number given by `$whichline.
	   The first line in the file corresponds to line number 0."
	#>
    $linenum = 0

    foreach($line in get-content $filename){
    if($whichline -eq $linenum){
    return $line
    }
    else{
    $linenum ++
    }
    }
}

#instructor solution
function q4($filename,$whichline) {
    <# Return the line of text from the file given by the `$filename
	   argument that corresponds to the line number given by `$whichline.
	   The first line in the file corresponds to line number 0."
	#>
$content = get-content $filename
return $content[$whichline]

}
############################5############################


function q5($path) {
    <# Return the child items from the given path sorted
       ascending by their Name
	#>
    get-childitem -path $path | sort-object
}

#instructor solution
function q5($path) {
    <# Return the child items from the given path sorted
       ascending by their Name
	#>
return get-childitem -path $path | sort-object-property name
}

############################6############################


function q6 {
    <# Return the sum of all elements provided on the pipeline
	#>
    param ( [parameter( ValueFromPipeline = $true )] [array]$pipelineInput)
    begin{
    $sum = 0
    }
    process{
    foreach($item in $pipelineInput){
        $sum += $item
    }
    }
    end{
    return $sum
    }

}

#instructor solution

function q6 {
    <# Return the sum of all elements provided on the pipeline
	#>
$sum = 0
foreach $a in $input){
$sum += $a
}
return $sum
}

#instructor solution 2

begin{$sum = 0}
process{$sum += $_}
end{return $sum}
############################7############################


function q7 {
	<# Return only those commands whose noun is process #>
    get-command -noun process

}

#instructor solution
function q7 {
	<# Return only those commands whose noun is process #>
return get-command -noun process
}



############################8############################


function q8($adjective) {
    <# Return the string 'PowerShell is ' followed by the adjective given
	   by the `$adjective argument
	#>    
    return "Powershell is "+$adjective
}

#instructor solution
function q8($adjective) {
    <# Return the string 'PowerShell is ' followed by the adjective given
	   by the `$adjective argument
	#>    
    return 'Powershell is '+$adjective
}


############################9############################



function q9($addr) {
	<# Return `$true when the given argument is a valid IPv4 address,
	   otherwise return `$false. For the purpose of this function, regard
	   addresses where all octets are in the range 0-255 inclusive to
	   be valid.
	#>
    $splitaddr = $addr.split(".")
    foreach($oct in $splitaddr){
    if($oct -lt 0 -or $oct -gt 255){
    return $false
    }
    }
    return $true
}

#instructor solution
function q9($addr) {
	<# Return `$true when the given argument is a valid IPv4 address,
	   otherwise return `$false. For the purpose of this function, regard
	   addresses where all octets are in the range 0-255 inclusive to
	   be valid.
	#>
<#
foreach($octet in $addr.split(".")){
if([int]$octet -lt 0 -or [int]$octet -gt 255){
return $false
}
}
return $true
#>
#instructor solution 2
if($addr.split(".")[0] -lt 0 -or $addr.split(".")[0] -gt 255){
return $false
}
elseif($addr.split(".")[1] -lt 0 -or $addr.split(".")[1] -gt 255){
return $false
}
elseif($addr.split(".")[2] -lt 0 -or $addr.split(".")[2] -gt 255){
return $false
}
elseif($addr.split(".")[3] -lt 0 -or $addr.split(".")[3] -gt 255){
return $false
}
return $true
}


############################10############################



function q10 ($filepath,$lasthash) {
    <# Return `$true if the contents of the file given in the
       `$filepath argument have changed since `$lasthash was
       computed. `$lasthash is the previously computed SHA256
       hash (as a string) of the contents of the file. #>
       $hash = (get-filehash -path $filepath -algorithm sha256).hash 
       if($lasthash -ceq $hash){
            return $false
       }
       elseif($lasthash -cne $hash){
            return $true
       }
}


#instructor solution
function q10 ($filepath,$lasthash) {
    <# Return `$true if the contents of the file given in the
       `$filepath argument have changed since `$lasthash was
       computed. `$lasthash is the previously computed SHA256
       hash (as a string) of the contents of the file. #>
return (get-filehash -path $filepath -algorithm sha256).hash -ne $lasthash
