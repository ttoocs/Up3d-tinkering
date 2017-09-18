# Up3d-tinkering
Playing around with up3d. 

# Upgrades sofar:
CMake'd, unified bin directory.

# TODO
* Get it working with up3d plus.
  * Run into 28k issue, simply ignoring all errors and uploading it all at once, will work to some degree. (It printed 80%? of a 1cm cube)

# Notes:
Depending on what configuration UP3D\_WriteBlocks() and upload.c are you can get different behaviours:
* With default UP3D\_WriteBlocks(), by changing the size of blocks[] in upload.c, you can get the upload to freeze at different values. Increasing it past the size of the read file, seems to let the whole thing upload, but then in upload.c check `UP3D_GetParameter(0xC6) == tblocks`, it will return 0 and fail to upload. If one ignores then tries to ignore this, it will start printing until hitting some point and freezing.
* By fudging the size of fblocks in up3d.c, you can also get the above to work. Note: Sometimes the call to getFreeBlocks does actually error.

Possible cases:
* Freezes on upload due to having no free blocks as returned by Up3d\_getfreeblocks();
* After upload, while waiting to verify the number of block's written, it only ever returns a 0.
* It'll start to print, and for small objects work, but after some time will freeze. (My guess this is around the 28Kb mark, or possibly dependent on the blocks[], but I'm not entirely sure about this.)


# Proceeding:
* It looks like some more knowledge of the actual protocol is needed, which would need to be captured through wireshark, and then decoded to some degree. (IE: reverse engineer the protocol)

