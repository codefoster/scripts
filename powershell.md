https://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/

``` powershell
# Create a new hard linked directory
cmd /c mklink /j <link> <target>
```

``` powershell
# Removing the hard linked directory
cmd /c rmdir <link>
```

``` powershell
# Azcopy files to Blob Storage
azcopy /Source:"D:\onedrive\videos\codefoster\microsoft virtual academy\introduction to jquery" /Dest:"https://onedrivearchive0001.blob.core.windows.net/archive/\videos\codefoster\microsoft virtual academy\introduction to jquery" /DestKey:UAP5SnUgZ7tj8YEXvsP7BHxHipQVfrlVwb9/6mRKq6Yz1mrDPDga5W21T47BqQ45xdAPbjXk2EmRzgVez2LOLA== /Pattern:"*.mp4" /S 
```

``` powershell
# List Cool Blobs and Set Tier For Each
az storage blob list -c archive --account-name 'onedrivearchive0001' --query "[?properties.blobTier == 'Cool'].name" -o table | Select-Object -Skip 2 | ForEach-Object { az storage blob set-tier --tier Archive -c archive -n "$_" --account-name onedrivearchive0001 }
```
