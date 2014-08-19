# README #

This repo contains build files for basic Apache-based Docker images, suitable
for many web applications or for use in deriving your own, more specific images.

Included are the following:  

- apache: A simple Apache install, including SSL support
- apache-php: The above, but including PHP5 support
- laravel: As apache-php, with the Laravel framework ready for your app code
- phalcon: As apache-php, with the Phalcon framework ready for your app code

Feel free to derive images from any of the above, which are available as
eboraas/apache, eboraas/apache-php, eboraas/laravel, and eboraas/phalcon. I
do try to keep the public builds as up-to-date as possible.

They are built, by default, against my Debian images, which are publicly available
via Docker Hub, and can thus be built as-is or retargeted against other Debian 
base images, if you prefer.

If you're interested, sources for my Debian images and instructions for
building your own can be found at:  
  https://bitbucket.org/EdBoraas/debian-docker

-Ed
