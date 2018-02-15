Tự dưng một số report trong GA của mình bị dính `(not set)` này mà chẳng biết truy tìm tung tích thế nào.

Nhờ lần mò nhiều nguồn và nhất là bài này tại LunaMetrics mà tìm ra được nguồn căn của nó.

> http://www.lunametrics.com/blog/2015/06/25/11-places-google-analytics-not-set/

Thường thì dễ bị `(not set)` nhất là:

1. Chuyển từ GA sang GTM nên tracker dễ bị lẫn lộn.
2. Spam từ Bot/Crawler.

Cách giải quyết là bật Secondary Dimension lên check thêm, như Hostname, Country, IP, Browser/Browser Version...
