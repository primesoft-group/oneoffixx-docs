[![Build Status](https://travis-ci.org/Sevitec/oneoffixx-docs.svg?branch=gh-pages)](https://travis-ci.org/Sevitec/oneoffixx-docs)

# Docs
Documentation Repository for OneOffixx

[Site](http://docs.oneoffixx.com)

## Dev Notes

Currently used theme: [WinStrap](https://github.com/winjs/winstrap) - with OneOffixx color as accent color.

Quick guide to change color theme:

Download node.js from https://nodejs.org/en/#download

Open cmd and run:

    npm install -g grunt-cli
    npm install -g bower

Open git bash at preferred Location and run:

    git clone https://github.com/winjs/winstrap.git

Change the $color_accent in winstrap\src\scss\win\_colors.scss.

In git bash, go into folder "winstrap" and run:

    grunt

Go to winstrap\dist\css and copy the files into oneoffixx-docs\assets\css

Push oneoffixx-docs to oneoffixx-docs github repo, refresh page, there you go.
