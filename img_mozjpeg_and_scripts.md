There is great tool (mozjpeg)[https://mozjpeg.com/] to optimize the Jpeg files without losing quality
To use it offline for many images use [offline mozjpeg](https://github.com/mozilla/mozjpeg/releases) (`mozjpeg-v4.0.3-win-x64` in my case)
Then use `cjpeg` (taken script from this [answer](https://superuser.com/questions/955916/how-to-batch-convert-jpeg-images-with-jpegtran-on-windows)) as below

```sh
// copy files from `src` folder to `out` folder with the same filename
for %f in (src/*.jpg) do cjpeg src/%f > out/%~nf.jpg 

// copy files from in the same folder with `_compressed` suffix for compressed files
for %f in (*.jpg) do cjpeg %f > %~nf_compressed.jpg 
```

https://stackoverflow.com/questions/39025850/powershell-modify-date-and-time-of-a-file-to-reflect-its-filename (my script based on this ) + [this](https://superuser.com/questions/924365/changing-last-modified-date-or-time-via-powershell)


```powershell
     foreach ($file in Get-ChildItem *.jpg)
     {
     $yy = $file.Name.substring(4,4)
     $mm = $file.Name.substring(8,2)
     $dd = $file.Name.substring(10,2)
     $hh = $file.Name.substring(13,2)
     $min = $file.Name.substring(15,2)
     $ss = $file.Name.substring(17,2)

    #Create a Date Time object based on the file name
    $date =  get-date -Year $YY -Month $MM -Day $DD -Hour $hh -Minute $min -Second $SS

    #Echo out to screen
    Write-Host "Setting $($file.BaseName) dateModified as $($Date.Date)"
    $file.LastWriteTime = $Date
    $file.CreationTime = $Date
    }
```

Rename files from Camera (or Action camera to the same format as from phone)
```powershell
     foreach ($file in Get-ChildItem *.mov)
     {
     $updName = $file.LastWriteTime.ToString("yyyyMMdd_HHmmss") 
     $cre = $file.CreationTime  
     $ext = $file.Extension  

    #Echo out to screen
    Write-Host "Created $($cre) dateModified as $($upd) $($ext) __ $($updName)"
     rename-item $file -newname "VID_$($updName)_NOT_phone$($ext)"
    }
```