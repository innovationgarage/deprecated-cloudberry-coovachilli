# cloudberry-covachilli

Configuration to be used with a cloudberry chilli deployment.

## Useful links

- [CoovaChilli captive portal](https://openwrt.org/docs/guide-user/services/captive-portal/wireless.hotspot.coova-chilli?s[]=coovachilli)
- [CoovaChilli - man pages](http://coova.github.io/CoovaChilli/man-pages.html)
- [Coova website](https://coova.github.io)

## Troubleshooting

- Chilli provides a lot of debug information that can be turned on by using the
  `--debug` flag.  The file to change for this is in `/etc/init.d/chilli` where
  you can look for the `start_chilli()` function.
- Restarting is not reliable and might not always work as expected, so try
  stopping and starting when doing configuration changes. Also verifying that
  chilli is running via `ps` is a good idea.
- Don't mix WAN and LAN.
