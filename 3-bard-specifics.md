## Add BARD Specifics

### Excercise 4

So far we have Fiji container running locally, but what if we want to deploy it to the BARD?
Let's go back to the Dockerfile.
1. The `LABEL` in the Dockerfile are specific to the BARD. As BARD is a desktop environment, it needs to know where to show the Fiji app in BARD and what to do when users click it.
2. oc.icon and oc.icondata tells BARD which logo image to use. oc.icondata takes a base64 string for the image file fiji_icon.svg. To obtain the base64 string, we use the following
   ``` cat fiji_icon.svg |base64 ```
3. oc.cat specify which category Fiji belongs to. BARD has these categories 'development', 'office', 'education', 'utilities' etc.
4. oc.template is the name of the template to use. FROM in the Dockerfile.
5. oc.name is the name of the application. oc.displayname is what is shown in the BARD desktop.
6. oc.launch is a unique X11 window class name. To find out the name, we can use the command ```wmctrl -lx```
7. oc.path specifies the location of the application's binary excutable.
8. oc.args are the arguments passed to the command in oc.path, if there's any.
9. oc.showinview tells BARD to place an icon of the application in its dock.

Now let's look at the bottom section of the Dockerfile

```
RUN for d in /usr/share/icons /usr/share/pixmaps ; do echo "testing link in $d"; if [ -d $d ] && [ -x /composer/safelinks.sh ] ; then echo "fixing link in $d"; cd $d ; /composer/safelinks.sh ; fi; done

RUN mkdir -p /etc/localaccount
RUN for f in passwd shadow group gshadow ; do if [ -f /etc/$f ] ; then  cp /etc/$f /etc/localaccount; rm -f /etc/$f; ln -s /etc/localaccount/$f /etc/$f; fi; done

```

Outside BARD, docker container runs as the USER specified in Dockerfile. BARD desktop allows users to log in via LDAP or OIDC, we need to run the docker container as the logged in user. The above commands makes the logged in user available inside the container.
