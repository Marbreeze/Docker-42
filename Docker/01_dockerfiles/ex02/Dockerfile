# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: mstratu <marvin@42.fr>                     +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2019/09/30 15:20:33 by mstratu           #+#    #+#              #
#    Updated: 2019/09/30 15:49:17 by mstratu          ###   ########.fr        #
#                                                                              #
# **************************************************************************** #
# 1. To be able to test first in your working directory build the Dockerfile that
#    you created and call the image ft-rails:5.0.2-on-build. This is the name that
#    will be identified once we run the "mini" Dockerfile
#       -> docker build -t ft-rails:5.0.2-on-build .
#
# 2. Then create a rails application of your choice in the same working directory
#       -> rails new my_app
#
# 3. You will then enter my_app and place the "mini" Dockerfile there.  This new
#    Docker file should call the image that you just built and pass CMD with
#
#    arguments.
#  > FROM        ft-rails:5.0.2-on-build
#  > CMD         ["rails", "s", "-b", " 0.0.0.0 "]
#
# 4. build this "mini" Dockerfile in this my_app folder
#       -> docker build -t ft-rails .
#
# 5. This will call the first image you built and install everything for you.
#    neat right? ^_^
#
# 6. Final step is to test it out.
#       -> docker run --interactive --publish 3000:3000 ft-rails
#
# Ruby container
FROM				ruby
# Install rails and create the rails application path.
# You'll also be needing sqlite3 and nodejs to be able to deploy
RUN					apt-get update && apt-get upgrade -y
RUN					apt-get install nodejs -y
RUN					gem install rails
RUN					mkdir -p /opt/app
# Add the application to the application path.
					#make a folder, -p - make another folder inside of a new folder, /opt/app - name of the folders

ONBUILD WORKDIR		/opt/app
ONBUILD ADD			. /opt/app
# Default Ruby on Rails port number
ONBUILD EXPOSE		3000
# Run bundle install to be able to install all the necessary gems in the Gemlock file
ONBUILD RUN			bundle install && rake db:from && rake db:to
					#bundle is the same as apt-get just for ruby on rails
ONBUILD RUN       rake db:migrate && rake db:seed

