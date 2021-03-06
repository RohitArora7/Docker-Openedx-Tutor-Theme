# Docker-Openedx-Theme

Docker Openedx Theme Location 

Lets talk about index_overlay.html (It works! Powered by Open edX®)

---- Original File location at Docker container location 

_openedx/edx-platform/lms/templates_

Now we have to update the theme -Indigo Theme (The place for all your online learning)

---- Updated location will be 

_/openedx/themes/indigo/lms/templates_

NOW

1. Clone the theme 

```bash
git clone https://github.com/overhangio/indigo
```
2. Render the theme (_rohit/indigo/theme/lms/templates_)
```bash
tutor config render --extra-config ./indigo/config.yml ./indigo/theme "$(tutor config printroot)/env/build/openedx/themes/indigo"
```
   Files goes to tutor location 

   _/home/rohit/.local/share/tutor/env/build/openedx/themes/indigo/lms/templates_

3. Rebuild open edx image only 
```bash
tutor local stop
docker container prune -f 
tutor images build openedx
tutor local start
```
4.  Restart platform
```bash
tutor local start -d
```
5. Activate theme
```bash
tutor local settheme indigo $(tutor config printvalue LMS_HOST) $(tutor config printvalue CMS_HOST)
```

Now Direct Edit Part 

Go to bash mode of the new lms container
```bash
docker exec -it  tutor_local_lms_1 bash
```
Now go to indigo theme folder which is just created and edit files 
```bash
cd /openedx/themes/indigo/lms/templates
vim index_overlay.html
```

To Revert back to original open edx theme
```bash
tutor local settheme default $(tutor config printvalue LMS_HOST) $(tutor config printvalue CMS_HOST)
```





