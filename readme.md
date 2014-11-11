AVerMedia Game Capture HD II - The RESTful web interface
========================================================


Documentation and code storage for the reverse engeneering of the AVerMedia
Game Capture HD II. In particular this is a documentation of the RESTful web
interface.

Initial Request:
```
% curl 'http://131.173.172.118:24170/eos/query/device_name_get'
{"response":{"result":"C285%09Game%20Capture%20HD%20II%09MyGameCaptureBox%095.0.0"}}%

```

Pairing (just ignore that. Things work without this):
```
% curl 'http://131.173.172.118:24170/eos/method/pairing' \
    --data 'your_id=08:d8:33:01:3c:ff&your_name=yanbochuangQ102&your_ip=131.173.196.2&your_sys=4.4.2'
```

end commands to the device (e.g. start capture):
```
% curl 'http://131.173.172.118:24170/eos/method/irkey_send' --data 'key_id=12'
ir key sned command send
```

Key id `12` is the capture button on the remote control. Here are some codes
for other buttons:

| ID |           Key |
| --:| -------------:|
|  1 |         power |
|  3 |          menu |
|  5 |            up |
|  6 |          down |
|  7 | left or right |
|  8 | left or right |
|  9 |            ok |
| 12 |       capture |

list files:

```
% curl 'http://131.173.172.118:24170/eos/method/get_files_infos' \
   --data 'file_name_path=/media/sda1/&start_index=0&end_index=5'
get files infos command send

% curl 'http://131.173.172.118:24170/eos/query/files_infos_get'
{
   "files_infos" : [
      {
         "parent_path" : "/media/sda1/"
      },
      {
         "thumb_size" : "8.9 KB",
         "file_type" : "1",
         "file_name" : "141111-1854.mp4",
         "date" : "2014/11/11 18:58:13",
         "file_length" : "239",
         "file_size" : "359.2 MB",
         "thumb_position" : "/media/sda1/.thumb/.141111-1854_thumb.jpg"
      }
   ]
}
```

count files by path:
```
% curl 'http://131.173.172.118:24170/eos/method/get_file_counts_by_path' \
   --data 'file_name_path=/media/sda1/'
get file counts by path command send

% curl 'http://131.173.172.118:24170/eos/query/file_counts_get_by_path'
{
   "response" : {
      "result" : "1"
   }
}
```
