# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: mstratu <marvin@42.fr>                     +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2019/09/30 14:34:34 by mstratu           #+#    #+#              #
#    Updated: 2019/09/30 14:35:59 by mstratu          ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

# From an alpine image you’ll add to your container your favorite text editor, vim or
# emacs, that will launch along with your container.

FROM alpine:latest

# Install some packages

RUN apk update && apk upgrade && apk add vim && apk add git && apk add gcc

# Set up some environment var to test with our vim

ENV	MY_NAME="marina"
ENV MY_EMAIL="marina@42.us.org"
ENV MY_WELCOME_MESAGE="Welcome to vim. you are now in your txt editor"

# echo the ENV var into a.txt file

RUN echo $MY_WELCOME_MESSAGE >> myfile.txt && echo $MY_NAME >> myfile.txt && echo $MY_EMAIL >> myfile.txt

# 5. We'll start our container inside vim in the myfile.txt file

ENTRYPOINT ["vim", "myfile.txt"]
