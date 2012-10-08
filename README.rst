dms is a UPnP DLNA "Digital Media Server". It runs from the terminal, and serves content directly from the filesystem from the working directory, or the path given. The SSDP component will broadcast and respond to requests on all available network interfaces.

dms serves an additional entry for videos with the suffix "/transcode". This entry corresponds to transcoded video data as mpeg2 PAL-DVD.

dms uses `ffprobe` to get media data such as bitrate and duration, and `ffmpeg` for video transoding.

.. image:: https://lh3.googleusercontent.com/-z-zh7AzObGo/UEiWni1cQPI/AAAAAAAAASI/DRw9IoMMiNs/w497-h373/2012%2B-%2B1

Installing
==========

To run dms, assuming ``$GOPATH`` and Go have been configured already::

    $ go get bitbucket.org/anacrolix/dms
    $ $GOPATH/bin/dms

Supported Players
=================

 * Probably all Panasonic Viera TVs.
 * Android's BubbleUPnP, MediaHouse 
 * VLC

Known Issues
============

Go doesn't provide access to a ``*net.UDPConn``'s underlying handle without calling ``dup``, which is not available on Windows. As a result, SSDP broadcast does not work on Windows, but the SSDP component will still respond to requests. Assuming all devices are playing fairly, dms will eventually appear on your other devices after they broadcast.

Samsung TVs may use an unsupported service action `X_GetFeatureList`. This has not been implemented in dms, and is reported to prevent its use on these TVs.

Some players will ignore directory entries with the ``/transcode`` suffix. This means transcoded content is not currently available.