### tunearpcache

Diese Rolle vergößert den ARP-Cache für Batman und sollte daher auf allen Servern ausgerollt werden, auf denen es ein Batman-Interface gibt.

Eine Vergrößerung des ARP-Cache führt zu weniger ARP-Requests und damit zu einer kleinen Reduzierung der Netzlast.
Batman hat zwar selbst einen ARP-Cache für IPv4, jedoch keinen für IPv6.
