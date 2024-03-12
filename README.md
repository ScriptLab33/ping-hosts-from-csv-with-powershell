# Ping CSV hosts list with powershell and save the online and offline hosts to respective arrays

```
$hostnames = (import-csv "hostnames.csv" -Header "HOSTNAME","USER").HOSTNAME
clear
$hostnames
#test if they are online, and then add online hosts to $online_hosts

$Global:online_hosts = @()
$Global:offline_hosts = @()

foreach ($hostpc in $hostnames) {
    if (test-connection $hostpc -count 1 -erroraction silentlycontinue) {write-host $hostpc Online! -foregroundcolor green; $online_hosts += $hostpc} else {write-host $hostpc Offline! -foregroundcolor yellow; $offline_hosts += $hostpc}
}

write-host `nOnline Hosts:
$Global:online_hosts

write-host `nOffline Hosts:
$Global:offline_hosts

foreach ($online_host in $online_hosts) {
    write-host Online host: $online_host
}

foreach ($offline_host in $online_hosts) {
    write-host Offline host: $offline_host
}
```
