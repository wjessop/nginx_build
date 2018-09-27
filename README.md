# Build Nginx

You will need a working Docker host. When you have that, clone this repo and run a command like this:

    docker build --compress --build-arg version=1.15.4 --build-arg maintainer="Will Jessop <will@willj.net>" --build-arg iteration=yourcompany~1 .

You can also specify the number of processors to build with if you want (It defaults to 8):

    --build-arg processors=4

Find the [latest version of Nginx here](http://nginx.org/en/download.html).

When it has run the final line of output will end up being something like:

    Successfully built 44d72d60275e

Getting the build file out of the image is a little convoluted. Grab that image id and substitute it in this command (careful, there are two substitutions):

    id=$(docker create 44d72d60275e); docker cp $id:/$(docker run --rm  -i 44d72d60275e ls / | grep nginx) .; docker rm $id

You should now have an nginx deb file in your current directory.
